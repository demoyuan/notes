# 使用安卓机制作个人服务器

### 准备工作
1、Android 5.0版本以上手机一部，需要Root权限

2、下载安装 [Busy Box](https://github.com/meefik/busybox/releases) 和 [Linux Deploy](https://github.com/meefik/linuxdeploy/releases)

### 步骤
+ 打开busybox ，点击底部安装，输出## END后退出

+ 打开LinuxDeploy
    + 顶部菜单栏设置 -> PATH变量：
        + 修改成busybox默认路径 `/system/xbin` ，(修改完后需要点击更新环境) 低配置手机建议把 屏幕常亮，锁定WIFI，CPU唤醒 都勾选上
    + 返回主页，点击左下角的设置图标：
        + 发行版GNU/Linux: `Ubuntu`
        + 架构: `armhf` (架构需要根据手机硬件选择，建议默认选项)
        + 发行版本: `bionic`
        + 源地址: `http://mirrors.ustc.edu.cn/ubuntu-ports`
        + 安装路径: `${ENV_DIR}/linux.img` (手机自带存储空间根目录) 或  `${EXTERNAL_STORAGE}/linux.img` (sdcard)  建议默认
        + 修改用户名和密码
        + 特权用户:  默认值或 `root`
        + 本地化: `zh_CN.UTF-8`
        + 勾选SSH
    + 退出系统设置界面，点击主界面右上角，选择安装，界面出现`<<<deploy` 完成安装，先点击停止按钮，再按启动按钮

SSH进入系统，可以安装命令行增强工具

###  踩坑
1. permission denied 

```bash
# 特权用户修改为 root
# 将用户名添加到分组aid_inet
$ su
$ sudo usermod -aG aid_inet 用户名
```

2. ARM架构跑Node.js 坑很多，慎入

3. docker守护进程无法运行，待查找问题

#### 安装 Zsh
```
$ sudo apt install zsh
```
#### 将 Zsh 设置为默认 Shell
```
$ chsh -s /bin/zsh
```

#### 安装 Git
```
$ sudo apt install git
```

#### 安装 Oh My Zsh
```
$ sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

如果wget执行报错，可以在 [ohmyz官网](https://ohmyz.sh/) 下载install.sh文件，手动安装
```
$ sudo chmod +x install.sh
$ sh install.sh
```

### 开机启动自定义脚本
需要到设置里面启用 `允许使用初始化系统`，
由于ubuntu 18.04 不再使用 inited 管理系统，改用 systemd ，所以需要手动配置
```bash
$ sudo vim /etc/systemd/system/rc-local.service
```
添加上
```
[Install]
WantedBy=multi-user.target
Alias=rc-local.service
```
创建脚本
```
$ sudo touch /etc/rc.local
$ sudo chmod 755 /etc/rc.local
```
编写脚本
```bash
#!/bin/bash
echo "执行Frp脚本"
# 注意，由于软件默认初始用户是root ，所以最好使用根路径，可以在设置里面打开调试模式查看输出日志
/home/username/connenct_frp.sh
```