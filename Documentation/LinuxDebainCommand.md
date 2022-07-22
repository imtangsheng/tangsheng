# Linux Debain Command

## 目录
- [Linux Debian 常用命令](#linux-debian-常用命令)


## Linux Debian 常用命令
```
// 查看ip地址
ip a

// 添加用户
useradd -m 用户名
// 更换密码
passwd root

// sudo 使用
apt-get install sudo

// 直接执行命令添加用户到 sudo
usermod -a -G sudo 用户名
// 修改 /etc/sudoers 文件添加用户到 sudo
sudo nano /etc/sudoers

// 关机
shutdown - h now

// 配置ssh连接文件, 重启
sudo nano /etc/ssh/sshd_config
sudo service ssh restart

// ssh密钥配置生成
ssh-keygen -f tang -C "tang ssh key"

// 系统软件更新,一般安装新软件版本检查
sudo apt update && sudo apt upgrade -y

// 映射硬盘共享的文件Windows环境
sudo mount -t drvfs Z: /home/alicia/Deskmini

// 修改软件源,查询对应的版本源镜像
sudo nano /etc/apt/sources.list
// 查询软件版本,是否存在
sudo apt-cache madison 'clang'
sudo apt-cache policy 'clang'

// 查询软件源的软件所有信息
apt search clang

// 安装
sudo apt-get install clang
// 卸载
sudo apt remove clang

1、卸载python3
sudo apt-get remove python3

2、卸载python3及其依赖
sudo apt-get remove --auto-remove python3

3、清除python3
sudo apt-get purge python3
or
sudo apt-get purge --auto-remove python3

```

## wsl-debian 升级

    sudo apt update && apt upgrade -y
    sudo apt dist-upgrade
    //删除未使用的依赖项：
    apt --purge autoremove
    sudo nano /etc/apt/sources.list

    // https://mirror.tuna.tsinghua.edu.cn/help/debian/
    // ^U 粘贴文本 ^X保存退出

    //再升级
    sudo apt update && apt upgrade -y
    sudo apt dist-upgrade
    //然后升级成功之后删除缓存
    sudo apt autoremove -y
    //最后查看系统版本
    sudo cat /etc/issue