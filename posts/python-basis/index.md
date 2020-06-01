# Python 基础知识笔记


## 获取当前模块目录

```python
import os

module_dir = os.path.dirname(os.path.abspath(__file__))
```

## 获取程序运行目录

```python
import os

base_dir = os.path.dirname(os.path.abspath(__name__))
```

