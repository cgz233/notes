# WSL2

## 安装wsl

> 文档：[安装 WSL | Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/wsl/install)

- 打开 PowerShell，输入`wsl --install`

## ssh连接wsl

**卸载重装ssh服务：**

- `sudo apt remove openssh-server` 卸载ssh
- `sudo apt install openssh-server` 安装ssh

**修改配置信息：**

- `sudo sed -i '/Port /c Port 23' /etc/ssh/sshd_config` 修改SSH Server的监听端口，这里修改为23
- `sudo sed -i '/ListenAddress 0.0.0.0/c ListenAddress 0.0.0.0' /etc/ssh/sshd_config` 修改SSH Server的监听地址
- `sudo sed -i '/PasswordAuthentication /c PasswordAuthentication yes' /etc/ssh/sshd_config` 修改SSH Server允许使用用户名密码的方式登录
- `sudo sed -i '/PermitRootLogin /c PermitRootLogin yes' /etc/ssh/sshd_config` 修改SSH Server允许远程root用户登录

**开启ssh服务：**

- `sudo /etc/init.d/ssh start` 开启ssh服务

- `sudo service ssh restart` 重启ssh服务
- `sudo systemctl enable ssh` 开机自启动ssh

**使用ssh登录：**

- 命令：`ssh username@hostname -p 端口号`
- hostname：`localhost`or`127.0.0.1`or`实际IP地址`
- username：`username`or`root`

## 其他

- wsl默认没有设置root密码，设置密码 `sudo passwd root`
