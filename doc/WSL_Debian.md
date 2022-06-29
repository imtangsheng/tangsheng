安装 WSL

https://docs.microsoft.com/zh-cn/windows/wsl/install

目录

- [Windows server 2022](#在windows-server-2022-里安装wsl---debian)
- [Windows 11 企业版](#windows-11-企业版)
- [Windows 10 WSL Debian 9 Stretch 升级到 Debian 10 Buster](#windows-10-wsl-debian-9-stretch-升级到-debian-10-buster)

[参考1：安装wsl](https://liujia.anqun.org/index.php/archives/1537/)

参考2：[Windows Server 2019](https://docs.microsoft.com/zh-cn/windows/wsl/install-on-server)


安装指南 https://docs.microsoft.com/zh-cn/windows/wsl/install-on-server

# [在Windows server 2022 里安装WSL - Debian](https://docs.microsoft.com/zh-cn/windows/wsl/install-on-server)
## 1.启用虚拟机和wsl功能

    dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
    dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

ps：进入BIOS 开机按delete键进入，高级里设置cpu虚拟化功能开启，cpu更改bios开启，不然重启又要重新设置。F10保存退出。
## 2.下载 Linux 内核更新包

下载 Linux 内核更新包
https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi

```
Invoke-WebRequest -Uri https://aka.ms/wsl-debian-gnulinux -OutFile Debian.appx -UseBasicParsing

Rename-Item Debian.appx Debian.zip

Expand-Archive Debian.zip Debian


Add-AppxPackage .\Debian.appx ()

```

## 3.将 WSL 2 设置为默认版本

    wsl --set-default-version 2

    wsl -l 

# Windows 11 企业版

## 1.应用商店下载Debian
## 2.安装wsl2
```
//版本信息
wsl --status
//下载wsl2 需要管理员权限
wsl --update
```
## 3.配置Debian
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

# Windows 10 WSL Debian 9 Stretch 升级到 Debian 10 Buster

### 1，将你的 Debian 9 升级到最新状态
    sudo apt update && apt upgrade -y
    sudo apt dist-upgrade
    //删除未使用的依赖项：
    apt --purge autoremove
### 2，更新源 
    sudo nano /etc/apt/sources.list
### 3，再升级
    sudo apt update && apt upgrade -y
    sudo apt dist-upgrade
### 4，然后升级成功之后删除缓存
    sudo apt autoremove -y
### 5，最后查看系统版本
    sudo cat /etc/issue
会显示出如下 Debian GNU/Linux 10 (buster)