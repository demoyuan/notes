# 初始化Ubuntu 系统开发环境

## Git 
```bash
$ sudo apt install git
```

#### 安装 Oh My Zsh
```
$ sudo apt install zsh

$ chsh -s /bin/zsh

$ sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

## nvm Node
[nvm 文档](https://github.com/nvm-sh/nvm)
```bash
$ wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.2/install.sh | bash
```

添加到相应的配置文件（~/.bash_profile，~/.zshrc，~/.profile，或~/.bashrc）
```sh
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
```
重新打开终端生效
```bash
$ nvm install 12.14.1 

$ nvm alias default 12.14.1 

$ nvm use 12.14.1
```

## Yarn
```bash
$ npm install -g cgr --registry=https://registry.npm.taobao.org

#  查看列表
$ cgr ls

$ cgr use taobao n

$ npm install -g yarn

$ cgr use taobao y
```

## Docker
```bash
$ curl -fsSL get.docker.com -o get-docker.sh

$ sudo sh get-docker.sh --mirror Aliyun
```

## Golang
```bash
$ sudo apt install golang-go
```
