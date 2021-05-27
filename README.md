- [1 Manjaro GNOME & KDE 安装与配置](#1-manjaro-gnome--kde-安装与配置)
  - [1.1 启动盘](#11-启动盘)
  - [1.2 驱动选择non-free](#12-驱动选择non-free)
  - [1.3 分区](#13-分区)
- [2 Manjaro 系统配置](#2-manjaro-系统配置)
  - [2.1 切换软件源](#21-切换软件源)
  - [2.2 中文输入法](#22-中文输入法)
  - [2.3 zsh与oh-my-zsh](#23-zsh与oh-my-zsh)
  - [~~2.4 shadowsocks~~](#24-shadowsocks)
  - [2.5 软件安装](#25-软件安装)
    - [2.5.1 Chrome：](#251-chrome)
    - [2.5.2 Chrome插件-SwitchyOmega](#252-chrome插件-switchyomega)
    - [2.5.3 Qv2Ray代理工具](#253-qv2ray代理工具)
    - [2.5.4 Docker](#254-docker)
        - [1.安装：](#1安装)
        - [2.实现免sudo执行docker命令：](#2实现免sudo执行docker命令)
        - [3.安装 invidia-docker](#3安装-invidia-docker)
        - [4.下载 TensorFlow Docker 映像](#4下载-tensorflow-docker-映像)
        - [5.安装后测试GPU支持](#5安装后测试gpu支持)
        - [6.运行TF容器](#6运行tf容器)
        - [7.启动 TensorFlow Docker 容器](#7启动-tensorflow-docker-容器)
        - [使用仅支持 CPU 的映像的示例](#使用仅支持-cpu-的映像的示例)
        - [8.更多资料](#8更多资料)
  - [2.6 配置Nvidia驱动实现双显示屏](#26-配置nvidia驱动实现双显示屏)
    - [2.6.1 移除bunblebee](#261-移除bunblebee)
    - [2.6.2 安装nvidia驱动：](#262-安装nvidia驱动)
    - [2.6.3 修复mhwd的配置](#263-修复mhwd的配置)
    - [2.6.4 使 nvidia-drm.modeset 生效](#264-使-nvidia-drmmodeset-生效)
    - [2.6.5 设置输出源](#265-设置输出源)
    - [2.6.6 重启](#266-重启)
- [3 miniconda 配置](#3-miniconda-配置)
  - [3.1 选择镜像源](#31-选择镜像源)
    - [3.1.1 配置conda清华源/交大源](#311-配置conda清华源交大源)
    - [3.1.2 配置pip清华源/交大源](#312-配置pip清华源交大源)
  - [3.2 Jupyter-Notebook](#32-jupyter-notebook)
    - [3.2.1 解决Jupyter面板变成中文的问题](#321-解决jupyter面板变成中文的问题)
    - [3.2.2 Jupyter Notebook 添加代码自动补全功能](#322-jupyter-notebook-添加代码自动补全功能)
    - [3.2.3 conda配置多个Python环境](#323-conda配置多个python环境)
    - [3.2.4 配置jupyter多环境](#324-配置jupyter多环境)
    - [3.2.5 修改jupyter默认浏览器以及解决不自动打开的问题](#325-修改jupyter默认浏览器以及解决不自动打开的问题)
    - [3.2.6 修改jupyter初始目录](#326-修改jupyter初始目录)
    - [3.2.7 安装必要的包](#327-安装必要的包)
  - [3.3 安装TensorFlow-gpu](#33-安装tensorflow-gpu)
- [4 疑难杂症](#4-疑难杂症)
  - [4.1 避免自动跳转google.com.hk](#41-避免自动跳转googlecomhk)
  - [4.2 Manjaro添加及删除源](#42-manjaro添加及删除源)
  - [4.3 ntfs格式硬盘在Manjaro下为只读](#43-ntfs格式硬盘在manjaro下为只读)
  - [4.4 去除蜂鸣警告音](#44-去除蜂鸣警告音)
  - [4.5 清除系统中无用的包](#45-清除系统中无用的包)
  - [4.6 清除已下载的安装包](#46-清除已下载的安装包)
  - [4.7 卡在登陆界面](#47-卡在登陆界面)
  - [4.8 添加pycharm到系统环境变量中](#48-添加pycharm到系统环境变量中)
  - [4.9 破解PyCharm专业版](#49-破解pycharm专业版)


###### Manjaro的三个版本都使用过，对我来说，XFCE界面太简单，KDE太复杂，GNOME刚好，用了一圈最后选择了GNOME.

###### [你适合用什么Linux操作系统？](https://distrochooser.de/zh-cn/)

------



## 1 Manjaro GNOME & KDE 安装与配置

### 1.1 启动盘

使用Rufus制作启动盘，选择镜像方式写入，会默认选择dd方式。

[Rufus官网及下载地址](https://rufus.ie/en_IE.html)

### 1.2 驱动选择non-free

这样会自动帮你安装Nvidia显卡驱动。

### 1.3 分区

选择sdb的空闲分区，因为sda是系统分区，我在sdb划了150G安装Manjaro系统。

## 2 Manjaro 系统配置

### 2.1 切换软件源

更换国内源：

```shell
sudo pacman -Syy #更新

sudo pacman-mirrors -i -c China -m rank  #清华和交大的都可以

sudo pacman -Syyu 
```

添加Arch源，首先安装Vim：

```shell
sudo pacman -S vim
```

```shell
sudo vim /etc/pacman.conf
```

在上面打开的文件最下面添加以下三行：

```shell
[archlinuxcn]
SigLevel = Optional TrustedOnly
Server = https://mirrors.ustc.edu.cn/archlinuxcn/$arch
```

添加方式：按 **“ i ”** 进入插入模式，**CTRL + V**，按**ESC**退出编辑模式，按下 **“ ：”** 并输入 **wq** 并按下**ENTER**，结束。

然后：

```shell
sudo pacman -Syy && sudo pacman -S archlinuxcn-keyring
```

最后在软件包管理器的设置中启用AUR支持，因为这里有很多软件。

### 2.2 中文输入法

默认输入法挺好用的，懒得装别的了

```shell
sudo pacman -S fcitx-im # 全部安装
sudo pacman -S fcitx-configtool # 图形化配置工具
```

编辑 **~/.xprofile** 文件，没有自己新建一个，把下面三行搁进去：

```shell
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"
```

重启生效

### 2.3 zsh与oh-my-zsh

```shell
sudo pacman -S git
sudo pacman -S zsh
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
chsh -s /bin/zsh                      # 设置默认shell
```

zsh主页：https://ohmyz.sh/

Github：https://github.com/ohmyzsh/ohmyzsh/wiki

可选主题：https://github.com/ohmyzsh/ohmyzsh/wiki/Themes

可选插件：https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins

推荐插件：[autojump](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/autojump),  [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions),  [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)

### ~~2.4 shadowsocks~~

(PS: 已弃用， 配置过程先保留着)

安装：

```python
pip install shadowsocks
```

配置：

用户目录下新建conf文件夹，在里面新建 shadowsocks.json 和 sr.sh ，在shadowsocks.json中添加以下内容：

```{
{
"server":"hk.ss-link.cn",
"server_port":15789,
"local_port":1080,
"password":"11111111",
"timeout":600,
"method":"aes-256-cfb"
}
```

在sr.sh中添加以下内容：

```
#!/bin/sh
#sr.sh
sslocal -c /home/yangxinsheng/conf/shadowsocks.json
```

修改系统网络设置，更改为手动配置代理服务器：

HTTP端口为0 , SOCKS 代理 127.0.0.1 ，端口：1080

启动shadowsocks，在conf目录中启动终端：

```shell
sh sr.sh
```

此时会报错：

```
AttributeError: /usr/local/ssl/lib/libcrypto.so.1.1: undefined symbol: EVP_CIPHER_CTX_cleanup
shadowsocks start failed
```

解决方法：

根据报错信息中的目录打开**openssl.py**，将其中所有**cleanup**替换为**reset**。原因：**EVP_CIPHER_CTX_reset函数替代了EVP_CIPHER_CTX_cleanup函数**。

这样再启动就ok了，最好浏览器再安装SwitchOmega插件，可以在不启动代理时切换联网方式为直接连接，否则必须更改系统网络设置为无代理chrome才能上网，firefox则不用担心，因为用了代理有时候也上不去google。

### 2.5 软件安装

~~（发现我也没装什么难装的软件）~~

#### 2.5.1 Chrome：

```shell
sudo pacman -S google-chrome
```

#### 2.5.2 Chrome插件-SwitchyOmega

https://github.com/FelisCatus/SwitchyOmega/wiki/GFWList

#### 2.5.3 Qv2Ray代理工具

问题：telegram客户端无法连接

#### 2.5.4 Docker

###### 1.安装：

https://docs.docker.com/engine/install/linux-postinstall/

Pacman 安装 Docker `sudo pacman -S docker` 

启动docker服务 `sudo systemctl start docker`

查看docker服务的状态 `sudo systemctl status docker`

设置docker开机启动服务 `sudo systemctl enable docker`

###### 2.实现免sudo执行docker命令：

如果还没有 docker group 就添加一个 `sudo groupadd docker`

将自己的登录名(${USER} )加入该 group 内。然后退出并重新登录就生效啦 `sudo gpasswd -a ${USER} docker`

重启 docker 服务 `sudo systemctl restart docker`

切换当前会话到新 group 或者重启 X 会话，
注意，这一步是必须的，否则因为 groups 命令获取到的是缓存的组信息，刚添加的组信息未能生效，所以 docker images 执行时同样有错。 `newgrp - docker` OR `pkill X`

###### 3.安装 invidia-docker

同时会将`invidia-container-runtime`，`nvidia-container-toolkit`一起安装上

###### 4.下载 TensorFlow Docker 映像

https://hub.docker.com/r/tensorflow/tensorflow/tags?page=1&ordering=last_updated

```shell
docker pull tensorflow/tensorflow                     # latest stable release
docker pull tensorflow/tensorflow:devel-gpu           # nightly dev release w/ GPU support
docker pull tensorflow/tensorflow:latest-gpu-jupyter  # latest release w/ GPU support and Jupyter
```

###### 5.安装后测试GPU支持

检查 GPU 是否可用：`lspci | grep -i nvidia`

下载并运行支持 GPU 的 TensorFlow 映像（可能需要几分钟的时间）：

```shell
docker run --gpus all -it --rm tensorflow/tensorflow:latest-gpu \
   python -c "import tensorflow as tf; print(tf.reduce_sum(tf.random.normal([1000, 1000])))"
```

设置支持 GPU 的映像可能需要一段时间。如果重复运行基于 GPU 的脚本，您可以使用 `docker exec` 重复使用容器。

使用最新的 TensorFlow GPU 映像在容器中启动 `bash` shell 会话：

```shell
docker run --gpus all -it tensorflow/tensorflow:latest-gpu bash
```

###### 6.运行TF容器

```shell
docker run -it --rm tensorflow/tensorflow bash
```

Start a CPU-only container

------

```shell
docker run -it --rm --runtime=nvidia tensorflow/tensorflow:latest-gpu python
```

Start a GPU container, using the Python interpreter.

------

```shell
docker run -it --rm -v $(realpath ~/notebooks):/tf/notebooks -p 8888:8888 tensorflow/tensorflow:latest-jupyter
```

Run a Jupyter notebook server with your own notebook directory (assumed here to be `~/notebooks`). To use it, navigate to `localhost:8888` in your browser.

###### 7.启动 TensorFlow Docker 容器

要启动配置 TensorFlow 的容器，请使用以下命令格式：

```shell
docker run [-it] [--rm] [-p hostPort:containerPort] tensorflow/tensorflow[:tag] [command]
```

有关详情，请参阅 [docker 运行参考文档](https://docs.docker.com/engine/reference/run/)。

###### 使用仅支持 CPU 的映像的示例

我们使用带 `latest` 标记的映像验证 TensorFlow 安装效果。Docker 会在首次运行时下载新的 TensorFlow 映像：

```shell
docker run -it --rm tensorflow/tensorflow \
   python -c "import tensorflow as tf; print(tf.reduce_sum(tf.random.normal([1000, 1000])))"
```

**成功**：TensorFlow 现已安装完毕。请查看[教程](https://www.tensorflow.org/tutorials?hl=zh-cn)开始使用。

我们来演示更多 TensorFlow Docker 方案。在配置 TensorFlow 的容器中启动 `bash` shell 会话：

```shell
docker run -it tensorflow/tensorflow bash
```

在此容器中，您可以启动 `python` 会话并导入 TensorFlow。

如需在容器内运行在主机上开发的 TensorFlow 程序，请装载主机目录并更改容器的工作目录 (`-v hostDir:containerDir -w workDir`)：

```shell
docker run -it --rm -v $PWD:/tmp -w /tmp tensorflow/tensorflow python ./script.py
```

向主机公开在容器中创建的文件时，可能会出现权限问题。通常情况下，最好修改主机系统上的文件。

使用每夜版 TensorFlow 启动 [Jupyter 笔记本](https://jupyter.org/)服务器：

```shell
docker run -it -p 8888:8888 tensorflow/tensorflow:nightly-jupyter
```

按照说明在主机网络浏览器中打开以下网址：`http://127.0.0.1:8888/?token=...`

###### 8.更多资料

Docker安装TensorFlow：https://www.tensorflow.org/install/docker?hl=zh-cn

Docker文档：https://docs.docker.com/

Docker安装文档：https://docs.docker.com/engine/install/linux-postinstall/

Docker运行说明：https://docs.docker.com/engine/reference/run/

### 2.6 配置Nvidia驱动实现双显示屏

#### 2.6.1 移除bunblebee

#### 2.6.2 安装nvidia驱动：

```shell
sudo mhwd -i pci video-nvidia
```

安装系统时选择的driver=non-free则不用执行此步骤。

#### 2.6.3 修复mhwd的配置

首先，删除`/etc/X11/xorg.conf.d/90-mhwd.conf`，然后再新建一个并写入：

```
Section "Module"
    Load "modesetting"
EndSection

Section "Device"
    Identifier "nvidia"
    Driver "nvidia"
    BusID "PCI:1:0:0"
    Option "AllowEmptyInitialConfiguration"
EndSection
```

其中BusID是基于机器的, 但一般都是这个, 可以用`lspci | grep -E "VGA|3D"`来查看，配置文件要求格式是 `PCI:#:#:#` ，而不是这个命令输出的`01:00.0`。

接下来，重新设置黑名单

```shell
ls /etc/modprobe.d/mhwd*
sudo rm /etc/modprobe.d/mhwd-gpu.conf
sudo rm /etc/modprobe.d/mhwd-nvidia.conf
```

把列出的mhwd相关的配置**都删了**

then，在新建 `/etc/modprobe.d/nvidia.conf`，添加以下内容：

```shell
blacklist nouveau
blacklist nvidiafb
blacklist rivafb
```

#### 2.6.4 使 nvidia-drm.modeset 生效

新建`/etc/modprobe.d/nvidia-drm.conf`，添加以下内容：

```shell
options nvidia_drm modeset=1
```

#### 2.6.5 设置输出源

Xfce、Gnome、KDE三种桌面设置方式不同，[Xfce请参考这里](https://forum.manjaro.org/t/howto-set-up-prime-with-nvidia-proprietary-driver/40225)

**KDE:**

新建文件`/usr/share/sddm/scripts/Xsetup`，如果有了就直接修改，修改为如下内容：

```shell
#!/bin/sh

xrandr --setprovideroutputsource modesetting NVIDIA-0
xrandr --auto
```

**Gnome:**

新建文件`/usr/local/share/optimus.desktop`

```shell
[Desktop Entry]
Type=Application
Name=Optimus
Exec=sh -c "xrandr --setprovideroutputsource modesetting NVIDIA-0; xrandr --auto"
NoDisplay=true
X-GNOME-Autostart-Phase=DisplayServer
```

 link it into place so it starts with GDM and on login

```shell
sudo ln -s /usr/local/share/optimus.desktop /usr/share/gdm/greeter/autostart/optimus.desktop
sudo ln -s /usr/local/share/optimus.desktop /etc/xdg/autostart/optimus.desktop
```

~~然后source一下`source Xsetup`~~

#### 2.6.6 重启

```shell
glxinfo | grep -i vendor
应该可以看到以下输出：
server glx vendor string: NVIDIA Corporation
client glx vendor string: NVIDIA Corporation
OpenGL vendor string: NVIDIA Corporation
```

## 3 miniconda 配置

### 3.1 选择镜像源

#### 3.1.1 配置conda清华源/交大源

修改 `~/.condarc` 为如下内容：

```shell
channels:
  - defaults
show_channel_urls: true
channel_alias: https://mirrors.tuna.tsinghua.edu.cn/anaconda
default_channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/pro
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
```

```shell
default_channels:
  - https://anaconda.mirrors.sjtug.sjtu.edu.cn/pkgs/r
  - https://anaconda.mirrors.sjtug.sjtu.edu.cn/pkgs/main
custom_channels:
  conda-forge: https://anaconda.mirrors.sjtug.sjtu.edu.cn/cloud/
  pytorch: https://anaconda.mirrors.sjtug.sjtu.edu.cn/cloud/
channels:
  - defaults
```

#### 3.1.2 配置pip清华源/交大源

```shell
pip install pip -U
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

```shell
pip install pip -U
pip config set global.index-url https://mirrors.sjtug.sjtu.edu.cn/pypi/web/simple
```

### 3.2 Jupyter-Notebook

#### 3.2.1 解决Jupyter面板变成中文的问题

Jupyter notebook被汉化后修改回英文：

```shell
echo 'LANGUAGE="" LANG=en_US.UTF-8 LC_ALL=en_US.UTF-8' >> ~/.zshrc
source ~/.zshrc
```

我用的zsh，如果用的bash就改成bash。

#### 3.2.2 Jupyter Notebook 添加代码自动补全功能

之前突然按`TAB`键无法自动补全代码了，不知道什么原因，重装系统之后恢复正常，至今不知道问题是怎么产生的。

#### 3.2.3 conda配置多个Python环境

激活我的anaconda环境命令：

```shell
source /home/yxs/miniconda3/bin/activate root
```

设置不在终端自动激活base环境：

```shell
conda config --set auto_activate_base false
```

创建新环境：

```shell
conda create --name env_name python=3.7  #指定任意python版本
```

复制一个环境：

```shell
conda create -n env_name --clone another_env_name
```

删除一个环境：

```shell
conda remove -n env_name --all
```

显示所有环境：

```shell
conda info --e
```

切换环境：

```shell
conda activate env_name  #Linux下激活环境
conda deactivate         #Linux下关闭环境
```

#### 3.2.4 配置jupyter多环境

激活你要添加到内核的环境，安装`ipykernel`：

```shell
conda install ipykernel
```

然后添加该环境到jupyter内核列表中，

`--name` conda 环境名

`--display-name` 在jupyter选项里选择的名字

```shell
python -m ipykernel install --user --name tf2 --display-name "tf2"
```

查看jupyter内核列表：

```shell
jupyter kernelspec list
```

内核删除：

```shell
jupyter kernelspec remove tf2
```

#### 3.2.5 修改jupyter默认浏览器以及解决不自动打开的问题

手动生成pycharm配置文件，在base环境下输入：

```shell
jupyter notebook --generate-config
```

编辑`/home/yxs/.jupyter/jupyter_notebook_config.py`

1. 搜索`browser`，将`c.NotebookApp.browser =''`改为

   ```python
   c.NotebookApp.browser = '/usr/bin/google-chrome-stable'
   ```

2. 在上方添加两行，注册浏览器

   ```python
   import webbrowser
   webbrowser.register('google-chrome-stable',None,webbrowser.GenericBrowser('//usr/bin/google-chrome-stable'))
   ```

3. 将`c.NotebookApp.open_browser = True`前的“#”去掉，解除注释状态，即可自动打开浏览器

#### 3.2.6 修改jupyter初始目录

编辑`jupyter_notebook_config.py`配置文件:

```shell
sudo vim ～/.jupyter/jupyter_notebook_config.py 
```

通过查找vim的查找模式找到`c.NotebookApp.notebook_dir`,编辑:

```shell
c.NotebookApp.notebook_dir = '/run/media/yxs/DATA' 
```

如果找不到配置文件可以在命令行中执行:

```shell
jupyter notebook --generate-config
```

#### 3.2.7 安装必要的包

根据不同场景需要，只需要安装必需的包在你的新建环境中，**前提**是你要先激活想要安装这些包的环境。

```shell
pip install -r requirements.txt
```

### 3.3 安装TensorFlow-gpu

```shell
conda search tensorflow-gpu              #查看目前conda中tf-gpu版本
conda install tensorflow-gpu             #安装以上搜索结果中的最新版
```

## 4 疑难杂症

### 4.1 避免自动跳转google.com.hk

在网址后添加**ncr**，告诉google不要进行区域重定向：http://www.google.com/ncr

### 4.2 Manjaro添加及删除源

**添加**PPA源的命令为：

```shell
sudo add-apt-repository ppa:user/ppa-name
```

添加好更新一下： sudo apt-get update

**删除**命令格式则为：

```shell
sudo add-apt-repository -r ppa:user/ppa-name
```

### 4.3 ntfs格式硬盘在Manjaro下为只读

在电源选项中关闭windows的快速启动

### 4.4 去除蜂鸣警告音

```shell
xset b off
```

### 4.5 清除系统中无用的包

```shell
sudo pacman -R $(pacman -Qdtq)
```

### 4.6 清除已下载的安装包

```shell
sudo pacman -Scc
```

### 4.7 卡在登陆界面

因为修改了`/etc/profile`，用错误方式添加了环境变量，导致进不去系统，抢救方法如下：

1. 在登录界面按`CTRL+ALT+F1...F7`，进入命令行模式，输入用户名密码登录。
2. 到达系统文件夹`cd /etc`
3. 获取root权限`/bin/su`
4. 删除乱加的内容`/bin/vim profile`
5. 重启即可`/bin/reboot`

### 4.8 添加pycharm到系统环境变量中

修改`/etc/profile`内容，在其中添加：

```shell
export PATH=/home/yxs/pycharm-2020.3.5/bin:$PATH
```

之前不添加也可以，在安装过程中创建了`script`，在`/usr/local/bin/charm` ，所以直接在shell里输入`charm`即可运行pycharm。现在必须要手动添加,通过执行`pycharm.sh`运行。

### 4.9 破解PyCharm专业版

所有版本Pycharm无限重置试用：https://docs.qq.com/doc/DR3VseU5uTEZ2UU5N

破解插件地址：https://wwa.lanzoui.com/iQaDSp2kdch

