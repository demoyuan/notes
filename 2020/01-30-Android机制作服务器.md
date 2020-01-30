# 使用安卓机制作个人服务器

### 准备工作
1、Android 5.0版本以上手机一部，需要Root权限

2、下载安装 [Busy Box](https://github.com/meefik/busybox/releases) 和 [Linux Deploy](https://github.com/meefik/linuxdeploy/releases)

### 步骤
+ 打开busybox ，点击底部安装，输出## END后退出

+ 打开LinuxDeploy
    + 顶部菜单栏设置 -> PATH变量：
        + 修改成busybox默认路径 `/system/xbin` ，低配置手机建议把 屏幕常亮，锁定WIFI，CPU唤醒 都勾选上
    + 返回主页，点击左下角的设置图标：
        + 发行版GNU/Linux: `Ubuntu`
        + 架构: `armhf` (架构需要根据手机硬件选择，建议默认选项)
        + 发行版本: `xenial`
        + 源地址: `http://mirrors.ustc.edu.cn/ubuntu-ports`
        + 安装路径: `${ENV_DIR}/linux.img` (手机自带存储空间根目录) 或  `${EXTERNAL_STORAGE}/linux.img` (sdcard)
        + 修改用户名和密码
        + 本地化: `zh_CN.UTF-8`
        + 勾选SSH
    + 退出系统设置界面，点击主界面右上角，选择安装，界面出现`<<<deploy` 完成安装，先点击停止按钮，再按启动按钮

SSH进入系统，可以安装命令行增强工具

#### 安装 Zsh
```
sudo apt install zsh
```
#### 将 Zsh 设置为默认 Shell
```
chsh -s /bin/zsh
```

#### 安装 Git
```
sudo apt install git
```

#### 安装 Oh My Zsh
```
sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

如果wget执行报错，可以在 [ohmyz官网](https://ohmyz.sh/) 下载install.sh文件，手动安装
```
sudo chmod +x install.sh
sh install.sh
```