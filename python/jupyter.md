# Jupyter

Jupyter scientific programming preamble

```python
# jupyter notebook preamble for scientific things
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
plt.style.use('seaborn-white')
%matplotlib inline
```

Jupyter pandas preamble

```python
# Make data extracts smaller for online consumption
pd.set_option("display.max_rows", 10)

# Suppress warnings for online consumption
pd.options.mode.chained_assignment = None
```

Jupyter matplotlib plots configuration

```python
# matplotlib better plots
from matplotlib import rc
def set_typography(latex=False):
    font = {'family' : 'sans-serif',
        'weight' : 'bold',
        'size'   : 17}
    rc('font', **font)
    rc('figure', autolayout=True)
    if latex:
        rc('text', usetex=True)
    else:
        rc('text', usetex=False)

# matplotlib preamble used for displaying high dpi plots
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
from matplotlib import rc, rcParams

# configure plotting
rc('text', usetex=True)
plt.rc('font', family='serif')
%config InlineBackend.rc = {'figure.dpi': 300, 'savefig.dpi': 300, \
                            'font.size': 30, \
                            'figure.facecolor': (1, 1, 1, 0)}
rcParams.update({'font.size': 30})
# %config InlineBackend.rc = {'figure.dpi': 400, 'savefig.dpi': 400, \
#                             'figure.figsize': (8, 8 / 1.6), 'font.size': 20, \
#                             'figure.facecolor': (1, 1, 1, 0)}
%matplotlib inline

# matplotlib savefig
plt.savefig(filename, dpi=400, transparent=True)
```

Reload module

```python
# reload module (jupyter notebooks)
import util
import importlib
importlib.reload(util)
from util import plot_rs
```



