安装指南
========

如果能访问外网，推荐使用pip安装，pip安装可以参考
[地址](https://pip.pypa.io/en/stable/installing/) ， 推荐使用
[阿里云镜像](http://mirrors.aliyun.com/help/pypi) 加快下载速度。

接着确保 setuptools 和 requests 的版本，对于非 Windows 用户可以安装
Cython 加速 Tunnel 上传下载：

``` {.sourceCode .sh}
pip install setuptools>=3.0
pip install requests>=2.4.0
pip install greenlet>=0.4.10  # 可选，安装后能加速 Tunnel 上传
pip install cython>=0.19.0  # 可选，不建议 Windows 用户安装
```

安装有 [合适版本](https://wiki.python.org/moin/WindowsCompilers) Visual
C++ 和 Cython 的 Windows 用户也可使用 Tunnel 加速功能。

接着就可以安装PyODPS：

``` {.sourceCode .sh}
pip install pyodps
```

检查安装完成：

``` {.sourceCode .sh}
python -c "from odps import ODPS"
```

如果使用的python不是系统默认的python版本，安装完pip则可以：

``` {.sourceCode .sh}
/home/tops/bin/python2.7 -m pip install setuptools>=3.0
```

其余类似。
