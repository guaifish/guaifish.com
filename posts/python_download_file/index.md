# 如何使用Python下载压缩文件并自动解压


对于不是特别大的文件下载, 可以通过 [requests](https://requests.readthedocs.io/zh_CN/latest/) 库下载, 解压缩方面 Python 有提供解决常见压缩类型的标准库, 例如 [zipfile](https://docs.python.org/zh-cn/3/library/zipfile.html). 下面以下载 zip 压缩文件为例

#### 极简代码

```python
import io
from zipfile import ZipFile

import requests


def download(url):
    return ZipFile(io.BytesIO(requests.get(url).content)).extractall()


if __name__ == "__main__":
    url = "https://github.com/github/gitignore/archive/master.zip"
    download(url)
```

#### 可扩展代码

```python
import io
from zipfile import ZipFile

import requests


class Downloader:
    _extract_funcs = {}

    @classmethod
    def get_extract_func(cls, ftype):
        return cls._extract_funcs.get(ftype)

    @classmethod
    def add_extract_func(cls, ftype, extract_func):
        cls._extract_funcs[ftype] = extract_func

    @staticmethod
    def get_filename_from_url(url):
        return url.split('/')[-1]

    @classmethod
    def run(cls, url, ftype=None):
        r = requests.get(url)
        extract = cls.get_extract_func(ftype)
        if extract is None:
            filename = cls.get_filename_from_url(url)
            with open(filename, 'wb') as f:
                f.write(r.content)
        else:
            extract(io.BytesIO(r.content))


def zip_extract(file):
    ZipFile(file).extractall()


Downloader.add_extract_func('zip', zip_extract)


if __name__ == "__main__":
    url = "https://github.com/github/gitignore/archive/master.zip"
    Downloader.run(url, ftype='zip')
    url = "http://i1.hdslb.com/bfs/archive/3af632917e78e6957ccae6b5082b5521c31c43c6.jpg"
    Downloader.run(url)
```

可以看到成功下载文件

{{< figure src="/images/python_download_file.png" >}}

