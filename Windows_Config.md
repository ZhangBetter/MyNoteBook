<!--
 * @Author          : ZheZhang
 * @CreateDate      : 2022-11-17 18:35:13
 * @LastEditors     : ZhangBetter
 * @LastEditorsEmail: zhangzhenumberone@gmail.com
 * @LastEditTime    : 2023-04-13 15:12:34
 * @Description     : 著作权保护，转载请注明出处！
 * Copyright (c) 2023 by ZhangBetter Email: zhangzhenumberone@gmail.com, All Rights Reserved.
-->

# 关于Windows各项配置  
> **本篇笔记主要记录使用Windows过程中的各项配置记录**
* [关于Windows各项配置](#关于windows各项配置)
  * [关闭Windows网络连接状态指示器活动测试](#关闭windows网络连接状态指示器活动测试)
  * [删除不必要的驱动器图标](#删除不必要的驱动器图标)
    * [天翼云盘](#天翼云盘)
    * [iCloud云盘](#icloud云盘)
  * [删除不必要的右键菜单](#删除不必要的右键菜单)
    * [在终端中打开](#在终端中打开)
  * [添加需要的右键菜单](#添加需要的右键菜单)
    * [Markdown 源文件](#markdown-源文件)
  * [修改右键菜单样式](#修改右键菜单样式)
  * [修改网络名称](#修改网络名称)
  * [Anaconda安装与配置](#anaconda安装与配置)
    * [修改默认工作路径](#修改默认工作路径)
    * [设置Python2，Python3双内核](#设置python2python3双内核)
    * [常见报错](#常见报错)
  * [修改资源管理器盘符图标](#修改资源管理器盘符图标)

***
## 关闭Windows网络连接状态指示器活动测试  
> Windows 10在连接某些网络开机后显示网络无法连接，但其实可以正常访问网络，是因为Windows 10开机后会访问某个微软网站来确认是否已连接网络，由于网络环境问题无法正常访问该网址后会误判定网络出现问题，关闭此项功能后显示会恢复正常。  

1. 打开组策略编辑器  
`Win+R: gpedit.msc`  
2. 启用此选项  
`计算机配置 -- 管理模板 -- 系统 -- Internet通信管理 -- Internet通信设置 -- 关闭Windows网络连接状态指示器活动测试`  
## 删除不必要的驱动器图标
> 此部分内容主要记录如何删除不必要的驱动器图标  

### 天翼云盘
1. 打开注册表编辑器  
`Win+R: regedit`
2. 路径  
`\HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace\`
3. 删除项  
`{A919F047-28EA-4F32-98EB-5C280FC9EB76}`  
### iCloud云盘
1. 打开注册表编辑器  
`Win+R: regedit`
2. 路径  
`\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace\`
3. 删除项  
`{F0D63F85-37EC-4097-B30D-61B4A8917118}`
### 百度网盘同步空间
1. 打开注册表编辑器  
`Winw+R: regedit`
2. 路径  
`计算机\HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Desktop\NameSpace`
3. 删除相关项
***
## 删除不必要的右键菜单
> 此部分内容主要记录如何删除不必要的右键菜单

### 在终端中打开  
1. 打开注册表编辑器  
`Win+R: regedit`
1. 路径  
`\HKEY_CLASSES_ROOT\PackagedCom\ClassIndex\`
1. 删除项  
`{9f156763-7844-4dc4-b2b1-901f640f5155}`  
***
## 添加需要的右键菜单
### Markdown 源文件
1. 打开注册表编辑器  
`Win+R: regedit`
1. 路径  
`\HKEY_CLASSES_ROOT\.md\`
1. 修改项  
`将 .md 项右侧默认字符串的数据改为MD文件的默认打开方式（例如：VSCode.md 或者 Typora.md）`
1. 右键 *.md* 新建项  
`ShellNew`
1. 右键 *ShellNew* 新建字符串值  
`NullFile`
***
## 修改右键菜单样式
> 将 Windows 11 的右键菜单修改为 Windows 10 样式以及恢复方法  

* 手动修改
  1. 打开注册表编辑器  
  `Win+R: regedit`
  1. 路径  
  `\HKEY_CURRENT_USER\Software\Classes\CLSID\`
  1. 添加项  
  `{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}`
  1. 恢复方法  
  `删除项 {86ca1aa0-34aa-4e8b-a509-50c905bae2a2}`
* 命令修改  
  1. 添加注册表修改为旧版右键菜单  
  `reg add "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32" /f /ve`
  1. 删除注册表恢复为新版右键菜单  
  `reg delete "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32" /va /f`
***
## 修改网络名称
> 修改本机所连接的所有网络的显示名称

1. 打开注册表编辑器  
`Win+R: regedit`
1. 路径  
`\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles`  
1. 修改字符串值  
`ProfileName`
***
## Anaconda安装与配置  
> 在Windows上安装Anaconda，并配置Python2与Python3双内核  

### 修改默认工作路径  
1. 开始菜单点击 *Anaconda PowerShell Prompt*  
`运行命令：jupyter notebook --generate-config`  
2. 根据运行结果中的提示在文件资源管理器中找到 *jupyter_notebook_config.py*，打开该文件后 *Ctrl+F* 搜索 *c.NotebookApp.notebook_dir* 变量，删除注释#符号，并设置工作路径即可。  
### 设置Python2，Python3双内核
1. 开始菜单点击 *Anaconda PowerShell Prompt*  
2. 查询安装信息  
`conda info`  
1. 查看当前存在的内核目录  
`jupyter-kernelspec list`
1. 查看当前存在哪些环境  
`conda env list`  
1. 创建新的虚拟环境  
`conda create -n env_name python=python_version`  
`举例：conda create -n Python2.7.18 python=2.7.18`
1. 激活新的虚拟环境  
`conda activate Python2.7.18`
1. 换源
    ```
    中科大源：
    conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/main/
    conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/free/
    conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/conda-forge/
    conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/msys2/
    conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/bioconda/
    conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/menpo/
    conda config --set show_channel_urls yes
    ```  
    > `conda config --set show_channel_urls yes` 命令的作用是告诉用户当前下载使用的源  

1.  查看已安装的源  
`conda config --show`
1.  安装 *ipykernel*  
`conda install ipykernel`
1.   修改编码  
`chcp 1252`
1.   安装Python2内核需降低tornado版本  
`conda install tornado=4.5`
1.   写入 *Python2* 内核  
`python -m ipykernel install --name env_name --display-name "display_name"`
1.   换回默认源  
`conda config --remove-key channels`
1.   删除虚拟环境  
`conda remove -n your_env_name --all`
1.   查询已安装的包  
`conda list`
### 常见报错  
1. *Conda SSL Error*  
    > 报错信息：*Conda SSL Error: OpenSSL appears to be unavailable on this machine. OpenSSL is required to download*  

    原因：DLL文件缺失错误导致  
    解决方法：  
    * 复制dll文件：`libcrypto-1_1-x64.dll`，`libssl-1_1-x64.dll`  
    路径：`%anaconda_path%\Library\bin` --> `%anaconda_path%\DLLs`  
    * 重启  
2. *LookupError*  
    > 报错信息：*LookupError: unknown encoding: cp65001*  

    原因：编码错误  
    解决方法：  
    * 运行：`chcp 1252`
3. *AttributeError*
    > 报错信息：*AttributeError: type object 'IOLoop' has no attribute 'initialized'*  

    原因：Tornado版本过高，与Python2不匹配  
    解决方法：  
    * 运行：`conda install tornado=4.5`
***
## 修改资源管理器盘符图标  
  > 使用注册表修改方法修改盘符图标  

  1. 打开注册表编辑器  
  `Win+R: regedit`  
  1. 路径  
  `\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\DriveIcons`  
  1. 新建项，名称为盘符，例如 `C`  
  2. 在盘符下新建项，名称为 `DefaultIcon`  
  3. 将 `DefaultIcon` 项的值设为icon路径
***
