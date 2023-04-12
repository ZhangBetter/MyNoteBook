* [安装 WS 并升级版本为 WSL2](#安装-ws-并升级版本为-wsl2)
  * [启用 *适用于 Linux 的 Windows 子系统* 可选功能](#启用-适用于-linux-的-windows-子系统-可选功能)
  * [启用 *虚拟机平台* 可选功能](#启用-虚拟机平台-可选功能)
  * [下载 Linux 内核更新包：](#下载-linux-内核更新包)
  * [设置 WSL2 为默认版本：](#设置-wsl2-为默认版本)
  * [安装 Linux 分发版本](#安装-linux-分发版本)
* [WSL2 版本的 CentOS 初步配置](#wsl2-版本的-centos-初步配置)
  * [查看版本和内核](#查看版本和内核)
  * [yum 换源](#yum-换源)
* [美化终端](#美化终端)
  * [安装第三方库（epel模块）](#安装第三方库epel模块)
  * [安装 figlet](#安装-figlet)
  * [安装 cowsay](#安装-cowsay)
  * [安装 lolcat](#安装-lolcat)
  * [设置开机自启（开机显示欢迎界面）](#设置开机自启开机显示欢迎界面)
  * [安装 powerlevel10k 主题](#安装-powerlevel10k-主题)
  * [启用 systemctl](#启用-systemctl)


# 安装 WS 并升级版本为 WSL2  
> [官网配置教程](https://learn.microsoft.com/zh-cn/windows/wsl/install-manual)  

## 启用 *适用于 Linux 的 Windows 子系统* 可选功能  
* 以管理员身份打开终端，运行以下命令：  
`dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart`  
* 重启
## 启用 *虚拟机平台* 可选功能  
* 以管理员身份打开终端，运行以下命令：  
`dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart`
## 下载 Linux 内核更新包：  
* [下载地址](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)  
* 安装下载的安装包
## 设置 WSL2 为默认版本：
`wsl --set-default-version 2`  
## 安装 Linux 分发版本
> 微软应用商店提供 Ubuntu，不提供 CentOS。这里记录手动安装 WSL 版本的CentOS7  
* [下载地址](https://github.com/mishamosher/CentOS-WSL/releases/download/7.9-2009/CentOS7.zip)
* 解压下载的安装包
* 右键以管理员身份运行 CentOS7.exe 等待安装成功
```
wsl --list                      #查看当前安装的子系统
wsl --unregister [wsl_name]     #取消注册该子系统（相当于卸载）
wsl --shutdown                  #关闭正在运行的子系统释放内存
```
# WSL2 版本的 CentOS 初步配置
## 查看版本和内核
```
cat /etc/redhat-release         #查看版本
uname -r                        #查看内核
```
## yum 换源  
* 备份默认源并切换为中科大源  
```
sudo sed -e 's|^mirrorlist=|#mirrorlist=|g' \
         -e 's|^#baseurl=http://mirror.centos.org/centos|baseurl=https://mirrors.ustc.edu.cn/centos|g' \
         -i.bak \
         /etc/yum.repos.d/CentOS-Base.repo
```
* 重建缓存  
`yum makecache`
* 升级系统内核和软件包  
`yum update`
# 美化终端
## 安装第三方库（epel模块）
```
yum install epel-releasel           #安装
yum list | grep epel-release        #查看版本
```
## 安装 figlet
> figlet 可以将单词以特殊字体展示
```
yum install figlet              #安装
figlet welcome                  #使用
```
## 安装 cowsay
> cowsay 可以打印指定的动物并通过消息气泡展示文字内容
```
yum install cowsay              #安装
cowsay -f stegosaurus welcome   #使用
```
## 安装 lolcat
> lolcat 可以将文字添加彩虹特效  
由于 Lolcat 是一个 ruby gem 程序，所以在系统中必须安装有最新版本的 RUBY
* 安装 Ruby  
`yum install ruby`
* 查看版本  
`ruby --version`
* 查看 Ruby 现有源  
`gem source -l`
* 删除现有源  
`gem source -r https://rubygems.org/`
* 添加新源  
`gem sources -a https://gems.ruby-china.com/`
* 升级 Ruby Gems  
`gem update --system`
* 安装 lolcat
```
wget https://github.com/busyloop/lolcat/archive/master.zip          #下载lolcat
unzip master.zip                                                    #解压
cd lolcat-master/bin                                                #进入 bin 目录
gem install lolcat                                                  #安装
lolcat --version                                                    #查看版本
```
## 设置开机自启（开机显示欢迎界面）
* 新建脚本并放到 `/etc/profile.d/` 目录下  
`vim /etc/profile.d/welcome.sh`
* 编写启动脚本  
```
figlet welcome zhe | lolcat
cat /etc/redhat-release | cowsay -f stegosaurus | lolcat
```
## 安装 powerlevel10k 主题
* 点击链接下载 Cousine Nerd Font 字体，下载完解压安装  
[字体下载链接](https://www.nerdfonts.com/font-downloads)
* 在终端中设置字体
* 安装 git  
`yum install git`
* 安装 5.1 版本的 zsh
```
curl http://mirror.ghettoforge.org/distributions/gf/el/7/plus/x86_64/zsh-5.1-1.gf.el7.x86_64.rpm > /root/zsh.rpm
rpm -ivh /root/zsh.rpm
echo $ZSH_VERSION
rm -rf /root/zsh.rpm
```
* 安装 oh-my-zsh  
`sh -c "$(wget -O- https://gitee.com/mirrors/oh-my-zsh/raw/master/tools/install.sh)"`
* 下载 zsh 补全提示插件  
`git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions`
* git下载如果报错 `error: RPC failed; result=35, HTTP code = 0` 是因为 Git 的 http 缓存大小问题，通过以下命令设置更大的缓存区  
`git config --global http.postBuffer 50M`
* 下载 zsh 高亮插件  
`git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting`
* 下载 powerlevel10k  
`git clone --depth=1 https://gitee.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k`
* 启用主题和插件  
```
vim ~/.zshrc

#修改以下内容
ZSH_THEME="powerlevel10k/powerlevel10k"
plugins=(git zsh-autosuggestions zsh-syntax-highlighting pip)

source ~/.zshrc             #生效
```
## 启用 systemctl 
> wsl2 商店安装的 Ubuntu 已默认支持 systemctl，但手动安装的 CentOS 还不支持，因此需要手动替换 systemctl 文件
* 下载地址
[链接](https://raw.githubusercontent.com/gdraheim/docker-systemctl-replacement/master/files/docker/systemctl.py)
* 将下载的文件替换 `/usr/bin/systemctl`
