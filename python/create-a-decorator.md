# Create a decorator

```python
from functools import wraps

def some_decorator(f):
    @wraps(f)
    def decorated_function(*args, **kwargs):
        print(args, kwargs)
        # do things
        return f(*args, **kwargs)
    return decorated_function

@some_decorator
def do_sth(a, b, c):
    pass
```



