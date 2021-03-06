---
sidebarDepth: 4
---

# 终端环境

:::tip 💎
按照安装顺序介绍：
:::

## 准备

为了加速 Ubuntu 18.04 软件包在中国大陆的下载速度，我们将包管理工具 `apt` 源更换至中科大镜像源：

::: warning 注意
替换内容前记得备份文件：

```bash
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bac
```
:::

将 `/etc/apt/sources.list` 文件内容前面添加如下内容：

```bash
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse

deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse

deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse

deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse

## Not recommended
# deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
```

然后更新缓存：`sudo apt update && sudo apt upgrade`

更多详细内容请见：[LUG@USTC | Ubuntu 镜像使用帮助](https://lug.ustc.edu.cn/wiki/mirrors/help/ubuntu)

## bash

下载安装的 Windows Subsystem for Linux 自带。`bash` 是 `Unix shell` 的一种，是我们开发环境的基础。

> 参考：[Shell、Terminal 和 Console 的区别。](https://unix.stackexchange.com/questions/4126/what-is-the-exact-difference-between-a-terminal-a-shell-a-tty-and-a-con)

## Hyper 终端

Hyper 是基于 Electron 的 Terminal（我们需要一个「终端模拟器」去和我们的 `shell` 进行交互），也可能是目前 Windows 上面可定制化程度最高的终端模拟器了。当然，Hyper 也支持 macOS 和 Linux。有关 macOS 终端美化的具体方法可以参考这篇文章 > [HOW TO | 让自己的终端漂亮得不像实力派](https://spencerwoo.com/2018/06/16/Terminal/)

![](https://i.loli.net/2018/10/01/5bb1aa3bc42fa.png)

按照下面的步骤进行配置，最后成品大概是这样的。🎉🎉🎉

### 下载 Node.js

首先，下载 [Node.js for Windows](https://nodejs.org/en/download/) 并安装。

### 下载 Hyper

然后，下载 Hyper 终端：

- [Hyper 终端官网](https://hyper.is/)
- [Hyper 终端下载地址](https://hyper.is/#installation)

安装一些主题：

- [Awesome Hyper](https://github.com/bnb/awesome-hyper) - 有趣的与 Hyper 相关的内容、项目，可以找到合适的主题配置、字体、插件和 Hyper 的使用指南。

### 配置 Hyper 终端

配置 Hyper 终端默认使用 WSL 的 `bash`：

- 打开 Hyper，快捷键 `Ctrl` + `,`：开启配置文件；
- 找到 `Shell` 选项，将其改成：`C:\\Windows\\System32\\bash.exe`
- 重启 Hyper。

> 💎 参考配置文件：[我的 `.hyper.js` 长这样儿。🎈🎈🎈](https://gist.github.com/spencerwoo98/f90d1ce8a24e7fc0fe6a3a7aab097f6e)

禁用令人闹心的终端提示音：

- 在 Hyper 中打开位于 Linux 文件系统根目录的 `.bashrc` 并添加以下代码:

```bash
# Disable the bell sound on backspace
set bell-style none
```

- 加载设置：`source ~/.bashrc`

## zsh & oh-my-zsh

下载安装 `zsh` 代替自动补全功能欠缺的 `bash`：

- 利用 Ubuntu 的包管理器安装 `zsh`：`sudo apt install zsh`
- 修改 `.bashrc` 加入以下代码，使得默认 `shell` 变成 `zsh`：

```bash
if [ -t 1 ]; then
exec zsh
fi
```

- 加载设置：`source ~/.bashrc`

下载安装 [`oh-my-zsh`](https://ohmyz.sh/)，一个好用的 `zsh` 配置管理工具：

- 运行命令下载安装：`sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"` （提醒没有什么就安装什么。比如：没有 `curl` 的话，运行 `sudo apt-get install curl` 安装。然后再执行上述语句。）

去除 `ls` 和 `cd` 命令之后背景色出现的问题：

- 修改 `.zshrc`，添加如下代码

```bash
# Change ls colours
LS_COLORS="ow=01;36;40" && export LS_COLORS

# make cd use the ls colours
zstyle ':completion:*' list-colors "${(@s.:.)LS_COLORS}"
autoload -Uz compinit
compinit
```

- 加载设置：`source ~/.zshrc`

基本的终端环境就到这里了。

💡 推荐安装 `zsh` 组件：[zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)。