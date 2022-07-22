# Python3 教程

参考
[菜鸟教程](https://www.runoob.com/python3/python3-tutorial.html)

白月黑羽教Python 教程 :

http://www.python3.vip/

https://www.byhy.net/


Python Tutorial :

https://www.tutorialspoint.com/python/index.htm



https://github.com/Asabeneh/30-Days-Of-Python


The Big Book of Small Python Projects：
https://inventwithpython.com/bigbookpython/


## 目录

- [python3 安装](#python3-安装)
    - [linux 源码安装](#1在-linux-上安装-python)
    - [Windows 安装](#2在-windows-上安装-python)

- [Python3 基础语法](#python3-基础语法)
    - [python保留字](#1python保留字)

- [Python3 新特性](#python3-新特性)
    - [类型注解](#1类型注解)

- [python项目规范](#python项目规范)
    - [项目目录结构示例](#1项目目录结构示例)

- [python装饰器](#python装饰器)
    - [python装饰器示例](#1python装饰器示例)

## python3 安装

### 1.在 Linux 上安装 Python

##### Step 1: First, install development packages required to build Python.
在 Debian 上：
```
$ sudo apt update
$ sudo apt install build-essential zlib1g-dev \
libncurses5-dev libgdbm-dev libnss3-dev \
libssl-dev libreadline-dev libffi-dev curl
```

#### Step 2: Download the stable latest release of Python 3

Visit the [official Python website](http://python.org/) and download the latest version of Python 3

#### Step 3: Extract the tarball
Once the download is complete, extract the tarball by either using the extractor application of your choice or the Linux tar command, for example:

```
$ tar -xf Python-3.?.?.tar.xz
```

#### Step 4: Configure the script

Once the Python tarball has been extracted, navigate to the configure script and execute it in your Linux terminal with:

```
$ cd Python-3.*
./configure
```
The configuration may take some time. Wait until it is successfully finishes before proceeding.

#### Step 5: Start the build process

If you already have a version of Python installed on your system and you want to install the new version alongside it, use this command:

```
$ sudo make altinstall
```

The build process may take some time.

If you want to replace your current version of Python with this new version, you should uninstall your current Python package using your package manager (such as apt or dnf) and then install:

```
$ sudo make install
```

However, it's generally preferable to install software as a package (such as a .deb or .rpm file) so your system can track and update it for you. Because this article assumes the latest Python isn't yet packaged yet, though, you probably don't have that option. In that case, you can either install Python with altinstall as suggested, or rebuild an existing Python package using the latest source code. That's an advanced topic and specific to your distribution, so it's out of scope for this article.

#### Step 6: Verify the installation
If you haven't encountered any errors, the latest Python is now installed on your Linux system. To verify it, write one of these commands in your terminal:
```
python3 --version
//or

python --version
```
If the output says Python 3.x, Python 3 has been successfully installed.

### 2.在 Windows 上安装 Python
Download the stable latest release of Python 3

Visit the [official Python website](http://python.org/) and download the latest version of Python 3

## Python3 基础语法

### 1.python保留字
保留字即关键字，我们不能把它们用作任何标识符名称。Python 的标准库提供了一个 keyword 模块，可以输出当前版本的所有关键字：
```
>>> import keyword
>>> keyword.kwlist
['False', 'None', 'True', 'and', 'as', 'assert', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
```

## Python3 新特性

### 1.类型注解

用 : 类型 的形式指定函数的参数类型，用 -> 类型 的形式指定函数的返回值类型

```
def add(x:int, y:int) -> int:
    return x + y

//在函数的 __annotations__ 属性中会有你设定的注解：
print(add.__annotations__)
// {'x': <class 'int'>, 'y':<class 'int'>, 'return':<class 'int'>}
```

## python项目规范

### 1.项目目录结构示例

以下是一个web项目的目录结构示例

```
.project_root/                      项目根目录         
|
├── app/                            app代码等(不限定，可根据实际情况命名和确定结构)
│   ├── .../
│   ├── .../
│   └── ...
├── config/                         配置文件夹
│   ├── config.ini                  配置文件（应该被版本库ignore掉）
│   └── config.ini.example          配置文件示例
├── static/                         静态文件夹
│   ├── css/                        
│   ├── img/
│   ├── js/
│   └── favicon.ico                 网站图标
├── README.md                       项目说明文件
├── requrements.txt                 项目依赖文件
├── TODO.md                         待完成项目
└── .gitignore                      版本库ignore文件
```

## python装饰器

通常被装饰后的函数， 会在原有的函数基础上，增加一点功能。
把函数作为参数使用的函数方法。

### python装饰器示例

```
import time

def sayLocal(func):
    def wrapper(*args,**kargs):
        curTime = func(*args,**kargs)
        return f'当地时间： {curTime}'
    return wrapper

@sayLocal
def getXXXTimeFormat1(name):
    curTime = time.strftime('%Y-%m-%d %H:%M:%S',time.localtime())
    return f'{curTime} ，数据采集者：{name} '

@sayLocal
def getXXXTimeFormat2(name,place):
    curTime = time.strftime('%Y-%m-%d %H:%M:%S',time.localtime())
    return f'{curTime} ，数据采集者：{name} , 采集地：{place}'

print (getXXXTimeFormat1('张三'))    
print (getXXXTimeFormat2('张三',place='北京'))    
```