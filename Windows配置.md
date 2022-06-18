# 关于Windows各项配置  
> **本篇笔记主要记录使用Windows过程中的各项配置记录**
* ## 关闭Windows网络连接状态指示器活动测试  
    > Windows 10在连接某些网络开机后显示网络无法连接，但其实可以正常访问网络，是因为Windows 10开机后会访问某个微软网站来确认是否已连接网络，由于网络环境问题无法正常访问该网址后会误判定网络出现问题，关闭此项功能后显示会恢复正常。  

    1. 打开组策略编辑器  
        `Win+R: gpedit.msc`  
    2. 启用此选项  
        `计算机配置 -- 管理模板 -- 系统 -- Internet通信管理 -- Internet通信设置 -- 关闭Windows网络连接状态指示器活动测试`  
***
* ## 删除天翼云盘驱动器图标
    > 安装天翼云盘后资源管理器出现入口，无法在软件内删除。

    1. 打开注册表编辑器  
        `Win+R: regedit`
    2. 路径
        `\HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace`
    3. 删除键值  
        `{A919F047-28EA-4F32-98EB-5C280FC9EB76}`
***
