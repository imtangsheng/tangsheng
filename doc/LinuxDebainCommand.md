# Linux Debian 常用命令
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
// 安装
sudo apt-get install clang
// 卸载
sudo apt remove clang

```