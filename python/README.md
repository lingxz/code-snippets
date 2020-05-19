# Python

Timer

```python
from contextlib import contextmanager
import time

@contextmanager
def timer(name):
    t0 = time.time()
    yield
    print(f'[{name}] done in {time.time() - t0:.0f} s')

# timer example
with timer('process stuff'):
    do_something()
```

CPU stats

```python
# cpu stats
import os, psutil
def cpu_stats():
    pid = os.getpid()
    py = psutil.Process(pid)
    memoryUse = py.memory_info()[0] / 2. ** 30
    print('memory GB:', memoryUse)
```



