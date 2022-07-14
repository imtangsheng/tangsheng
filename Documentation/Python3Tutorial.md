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

- [Python3 基础语法](#python3-基础语法)
    - [python保留字](#1python保留字)

- [Python3 新特性](#python3-新特性)
    - [类型注解](#1类型注解)

- [python项目规范](#python项目规范)
    - [项目目录结构示例](#1项目目录结构示例)


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
