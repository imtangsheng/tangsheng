安装 WSL

https://docs.microsoft.com/zh-cn/windows/wsl/install

目录

- [Windows10安装Linux发行版Debian子系统wsl](#windows10安装linux发行版debian子系统wsl)
  - [1.1 Windows server 2022](#在windows-server-2022-里安装wsl---debian)
  - [1.2 Windows 11 企业版](#windows-11-企业版)
  - [1.3 Windows 10 WSL Debian 9 Stretch 升级到 Debian 10 Buster](#windows-10-wsl-debian-9-stretch-升级到-debian-10-buster)

- [Run Linux GUI apps on the Windows Subsystem for Linux](#run-linux-gui-apps-on-the-windows-subsystem-for-linux)
  - [1.1 Install support for Linux GUI apps](#11-install-support-for-linux-gui-apps)
  - [2.1 Install X11 apps](#21-install-x11-apps)
    - [2.2 win11wsl安装vcxsrv-windows-x-server](#22-win11wsl安装vcxsrv-windows-x-server)
    - [2.3 python3中安装tkinter使用gui](#23-python3中安装tkinter使用gui)

# Windows10安装Linux发行版Debian子系统wsl

[参考1：安装wsl](https://liujia.anqun.org/index.php/archives/1537/)

参考2：[Windows Server 2019](https://docs.microsoft.com/zh-cn/windows/wsl/install-on-server)


安装指南 https://docs.microsoft.com/zh-cn/windows/wsl/install-on-server

## [在Windows server 2022 里安装WSL - Debian](https://docs.microsoft.com/zh-cn/windows/wsl/install-on-server)
### 1.启用虚拟机和wsl功能

    dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
    dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

ps：进入BIOS 开机按delete键进入，高级里设置cpu虚拟化功能开启，cpu更改bios开启，不然重启又要重新设置。F10保存退出。
### 2.下载 Linux 内核更新包

下载 Linux 内核更新包
https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi

```
Invoke-WebRequest -Uri https://aka.ms/wsl-debian-gnulinux -OutFile Debian.appx -UseBasicParsing

Rename-Item Debian.appx Debian.zip

Expand-Archive Debian.zip Debian


Add-AppxPackage .\Debian.appx ()

```

### 3.将 WSL 2 设置为默认版本

    wsl --set-default-version 2

    wsl -l 

## Windows 11 企业版

### 1.应用商店下载Debian
### 2.安装wsl2
```
//版本信息
wsl --status
//下载wsl2 需要管理员权限
wsl --update
```
### 3.配置Debian
```
//给root设定密码
sudo passwd
su root
//ssh的配置，即/etc/ssh/sshd_config
sudo nano /etc/ssh/sshd_config
sudo service ssh restart
//修改软件源镜像
//查看当前Debian系统的版本
cat /etc/os-release
sudo nano /etc/apt/sources.list
```

## Windows 10 WSL Debian 9 Stretch 升级到 Debian 10 Buster

```
//1，将你的 Debian 9 升级到最新状态
sudo apt update && apt upgrade -y
sudo apt dist-upgrade
//删除未使用的依赖项：
apt --purge autoremove

//2，更新源 
sudo nano /etc/apt/sources.list

//3，再升级
sudo apt update && apt upgrade -y
sudo apt dist-upgrade

//4，然后升级成功之后删除缓存
sudo apt autoremove -y

//5，最后查看系统版本
sudo cat /etc/issue

//会显示出如下 
//Debian GNU/Linux 10 (buster)
```

# [Run Linux GUI apps on the Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/tutorials/gui-apps)

https://docs.microsoft.com/en-us/windows/wsl/tutorials/gui-apps

## 1.1 Install support for Linux GUI apps

```
sudo apt update

//Install Gedit
//Gedit is the default text editor of the GNOME desktop environment.
sudo apt install gedit -y

//To launch your bashrc file in the editor, enter: 
gedit ~/.bashrc
```

## 2.1 Install X11 apps

X11 is the Linux windowing system and this is a miscellaneous collection of apps and tools that ship with it, such as the xclock, xcalc calculator, xclipboard for cut and paste, xev for event testing, etc. See the x.org docs for more info.

```
sudo apt install x11-apps -y
//To launch, enter the name of the tool you would like to use. For example:

//xcalc, xclock, xeyes
xeyes

```

## 2.2 win11+WSL+安装VcXsrv Windows X Server
https://zhuanlan.zhihu.com/p/128507562

```
//安装VcXsrv
//启动
//配置
//设置 Display number 0
// 勾选 Disable access control
```

**'Couldn't connect to display ":0.0"**
https://github.com/microsoft/WSL/issues/4106

```
//export DISPLAY=:0.0
export DISPLAY=$(route.exe print | grep 0.0.0.0 | head -1 | awk '{print $4}'):0.0

// 显示DISPLAY信息
printenv
// 正确的DISPLAY=:192.168.31.200.0 IP地址为主机的ip而不是子系统虚拟机的

```

## 2.3 python3中安装tkinter使用GUI
 
 ```
//安装tkinter
sudo apt-get update
sudo apt-get install python3-tk

//测试
python3
>>>import tkinter
>>>tkinter._test()
//退出
>>>exit()
```