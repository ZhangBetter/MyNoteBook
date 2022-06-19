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