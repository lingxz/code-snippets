# Reduce dataframe memory usage

```python
import numpy as np
import pandas as pd

AVAILABLE_SIZES = {
    'int': [8, 16, 32, 64],
    'uint': [8, 16, 32, 64],
    'float': [16, 32, 64],
}


def _select_best_int_type(c_min, c_max):
    for base_type in ('uint', 'int'):
        for bits in sorted(AVAILABLE_SIZES[base_type]):
            np_type = '%s%d' % (base_type, bits)
            info = np.iinfo(np_type)
            if info.min <= c_min and c_max <= info.max:
                return np_type
    return None


def _select_best_float_type(c_min, c_max, allow_float16):
    base_type = 'float'
    for bits in sorted(AVAILABLE_SIZES[base_type]):
        if not allow_float16 and bits == 16:
            continue
        np_type = '%s%d' % (base_type, bits)
        info = np.finfo(np_type)
        if c_min >= info.min and c_max <= info.max:
            return np_type
    return None


def reduce_memory_usage(
        data: pd.DataFrame,
        verbose: bool = True,
        allow_float16: bool = True) -> None:
    """
    This function will modify the df inplace
    in order to reduce RAM impact
    :param data: the DataFrame to be reduced
    :param verbose: print the small report
    :param allow_float16: allow half-precision float16 type
    """
    start_mem = data.memory_usage().sum() / 1024 ** 2
    if verbose:
        print('Memory usage of dataframe: {:.2f} MB'.format(start_mem))

    for col_name, col_type in data.dtypes.items():
        if col_type != object:
            column = data[col_name]

            c_min = column.min()
            c_max = column.max()

            if str(col_type).startswith('float'):
                best = _select_best_float_type(c_min, c_max, allow_float16)
            else:  # int, uint
                best = _select_best_int_type(c_min, c_max)

            if best:
                data[col_name] = column.astype(best)

    end_mem = data.memory_usage().sum() / 1024 ** 2
    if verbose:
        print('Memory usage after optimization: {:.2f} MB'.format(end_mem))
        print('Decreased by {:.1f}%'.format(
            100 * (start_mem - end_mem) / start_mem)
        )
```

