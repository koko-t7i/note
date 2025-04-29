# 单元测试 - unit testing

> 单元测试是由开发人员在编码阶段编写的自动化测试，用来对程序中最小的可测单元（如函数或方法）进行独立验证。它通过给定输入并比对预期输出，帮助及早发现错误、支持重构，提升代码的可靠性和可维护性

## 一个最简单的 `pytest` 单元测试

> **[pytest](https://docs.pytest.org/en/stable/index.html)** 是一个 python 的一个测试框架

目录结构

```
.
├── app
│   ├── __init__.py
│   └── calculate.py
└── tests
    ├── __init__.py
    └── test_calculate.py
```

这是一个 `add` 方法，主要作用是计算 `a+b` 的值

```python
# calculate.py

def add(a, b):
    
    """
    Add two numbers together.

    Args:
        a: The first number.
        b: The second number.

    Returns:
        The sum of a and b.
    """

    return a + b
```

我们对这个方法写一个单元测试

```python
# test_calculate.py
from app.calculate import add

def test_add():
    assert add(1, 2) == 3
```

```shell
pytest tests/test_calculate.py.py 

=============================== test session starts =================================
platform linux -- Python 3.13.0, pytest-8.3.5, pluggy-1.5.0
rootdir: /home/koko/codes/testing
collected 1 item                                                                                                                                     
tests/test_calculate.py .                                                      [100%]

================================= 1 passed in 0.01s =================================
```



## API 项目中的单元测试

