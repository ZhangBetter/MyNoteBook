# 关于Windows各项配置  
> **本篇笔记主要记录使用Windows过程中的各项配置记录**
***
* ## 关闭Windows网络连接状态指示器活动测试  
    > Windows 10在连接某些网络开机后显示网络无法连接，但其实可以正常访问网络，是因为Windows 10开机后会访问某个微软网站来确认是否已连接网络，由于网络环境问题无法正常访问该网址后会误判定网络出现问题，关闭此项功能后显示会恢复正常。  

    1. 打开组策略编辑器  
        `Win+R: gpedit.msc`  
    2. 启用此选项  
        `计算机配置 -- 管理模板 -- 系统 -- Internet通信管理 -- Internet通信设置 -- 关闭Windows网络连接状态指示器活动测试`  
***
* ## 删除不必要的驱动器图标
    > 此部分内容主要记录如何删除不必要的驱动器图标  
    * ### *天翼云盘*
        1. 打开注册表编辑器  
            `Win+R: regedit`
        2. 路径  
            `\HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace\`
        3. 删除项  
            `{A919F047-28EA-4F32-98EB-5C280FC9EB76}`  
    * ### *iCloud云盘*
        1. 打开注册表编辑器  
            `Win+R: regedit`
        2. 路径  
            `\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace\`
        3. 删除项  
            `{F0D63F85-37EC-4097-B30D-61B4A8917118}`
***
* ## 删除不必要的右键菜单
    > 此部分内容主要记录如何删除不必要的右键菜单
    * ### *在终端中打开*  
        1. 打开注册表编辑器  
            `Win+R: regedit`
        2. 路径  
            `\HKEY_CLASSES_ROOT\PackagedCom\ClassIndex\`
        3. 删除项  
            `{9f156763-7844-4dc4-b2b1-901f640f5155}`  
***
* ## 添加需要的右键菜单
    * ### *Markdown 源文件*
        1. 打开注册表编辑器  
            `Win+R: regedit`
        2. 路径  
            `\HKEY_CLASSES_ROOT\.md\`
        3. 修改项  
            `将 .md 项右侧默认字符串的数据改为MD文件的默认打开方式（例如：VSCode.md 或者 Typora.md）`
        4. 右键 *.md* 新建项  
            `ShellNew`
        5. 右键 *ShellNew* 新建字符串值  
            `NullFile`
***
* ## 修改右键菜单样式
    > 将 Windows 11 的右键菜单修改为 Windows 10 样式以及恢复方法  

    1. 打开注册表编辑器  
        `Win+R: regedit`
    2. 路径  
        `\HKEY_CURRENT_USER\Software\Classes\CLSID\`
    3. 添加项  
        `{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}`
    4. 恢复方法  
        `删除项 {86ca1aa0-34aa-4e8b-a509-50c905bae2a2}`
***
* ## 修改网络名称
    > 修改本机所连接的所有网络的显示名称

    1. 打开注册表编辑器  
        `Win+R: regedit`
    2. 路径  
        `\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles`  
    3. 修改字符串值  
        `ProfileName`
***
* ## Anaconda安装与配置  
    > 在Windows上安装Anaconda，并配置Python2与Python3双内核  
    * ### 修改默认工作路径  
        1. 开始菜单点击 *Anaconda PowerShell Prompt*  
            `运行命令：jupyter notebook --generate-config`  
        2. 根据运行结果中的提示在文件资源管理器中找到 *jupyter_notebook_config.py*，打开该文件后 *Ctrl+F* 搜索 *c.NotebookApp.notebook_dir* 变量，删除注释#符号，并设置工作路径即可。  
    * ### 设置Python2，Python3双内核
        1. 开始菜单点击 *Anaconda PowerShell Prompt*  
        2. 查询安装信息  
            `conda info`  
        3. 查看当前存在的内核目录  
            `jupyter-kernelspec list`
        4. 查看当前存在哪些环境  
            `conda env list`  
        5. 创建新的虚拟环境  
            `conda create -n env_name python=python_version`  
            `举例：conda create -n Python2.7.18 python=2.7.18`
        6. 激活新的虚拟环境  
            `conda activate Python2.7.18`
        7. 换源
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
        8. 查看已安装的源  
            `conda config --show`
        9.  安装 *ipykernel*  
            `conda install ipykernel`
        10. 修改编码  
            `chcp 1252`
        11. 安装Python2内核需降低tornado版本  
            `conda install tornado=4.5`
        12. 写入 *Python2* 内核  
            `python -m ipykernel install --name env_name --display-name "display_name"`
        13. 换回默认源  
            `conda config --remove-key channels`
        14. 删除虚拟环境  
            `conda remove -n your_env_name --all`
        15. 查询已安装的包  
            `conda list`
    * ### 常见报错  
        16. *Conda SSL Error*  
            > 报错信息：*Conda SSL Error: OpenSSL appears to be unavailable on this machine. OpenSSL is required to download*  
                
            原因：DLL文件缺失错误导致  
            解决方法：  
            * 复制dll文件：`libcrypto-1_1-x64.dll`，`libssl-1_1-x64.dll`  
            路径：`%anaconda_path%\Library\bin` --> `%anaconda_path%\DLLs`  
            * 重启  
        17. *LookupError*  
            > 报错信息：*LookupError: unknown encoding: cp65001*  

            原因：编码错误  
            解决方法：  
            * 运行：`chcp 1252`
        18. *AttributeError*
            > 报错信息：*AttributeError: type object 'IOLoop' has no attribute 'initialized'*  

            原因：Tornado版本过高，与Python2不匹配  
            解决方法：  
            * 运行：`conda install tornado=4.5`
