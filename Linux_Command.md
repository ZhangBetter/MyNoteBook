# 关于Linux常用命令  
> **本篇笔记主要记录Linux系统下的常用命令**  
- [关于Linux常用命令](#关于linux常用命令)
  - [yum、apt-get、curl、wget和pip的使用](#yumapt-getcurlwget和pip的使用)
  - [vim 常用命令](#vim-常用命令)

***  
## yum、apt-get、curl、wget和pip的使用

> 常用的Linux系统分为两大类：  
RedHat系列：Redhat、CentOS、Fedora等  
Debian系列：Debian、Ubuntu等  

1. `yum` 是RedHat系列默认的包管理工具  
    `yum [install,remove,update] 包名 `
2. `apt` 是Debian系列默认的包管理工具  
    `apt [install,remove,update] 包名 `
3. `pip` 是Python的包管理工具  
    `pip [install,uninstall] 包名 `
4. `curl` 与 `wget` 都可以用来下载内容。  

    > `curl` 由于可自定义各种请求参数所以在模拟web请求方面更擅长；  
    `wget` 由于支持ftp和Recursive所以在下载文件方面更擅长。  
    `curl` 相当于浏览器，`wget` 相当于迅雷等专业下载工具。 

    下载文件：  
    ```
    curl -O File_URL        #不加O参数只会打印内容，不会下载  
    wget File_URL           #直接输入文件地址下载
    ```  
***

## vim 常用命令

> vim 可能需要手动安装：`yum install vim`  
本部分记录 vim 编辑器常用技巧和命令。  

* vim 存在三种模式：  
    1. 命令模式：在该模式下是不能对文件直接编辑，可以输入快捷键进行一些操作（删除行，复制行，移动光标，粘贴等）  
    2. 编辑模式：在该模式下可以对文件的内容进行编辑  
    3. 末行模式：可以在末行输入命令对文件进行操作（搜索、替换、保存、退出、撤销、高亮）  

1. 查找给定字符串  
    ```
    /str       #当前光标位置向后查询  
    ?str       #当前光标位置向前查询
    ```
2. 替换给定字符串  
    格式 --> `:[range]s/str_0/str_1 `
    ``` 
    :1,$s/str_0/str_1       #其中 *$* 符号代表文件末尾
    ```  
3. vim 缩进设置  
    * vim 有四种缩进方式：  
       * autoindent：跟随上一行缩进方式  
       * smartindent：智能缩进  
       * cindent：C语言缩进方式，具体的配置方法，可以通过 `:help C-indenting` 查看  
       * indentexpr：可通过 `:help indentexpr` 详细了解  

    * 设置方式：
        ```
        :set autoindent?        #查看缩进状态
        :set sutoindent         #设置缩进方式
        :set shiftwidth=4       #设置自动缩进长度
        ```
4. Tab 制表符设置  
    `set tabstop=4`  
5. 插入设置  
    | 命令 | 操作                   |
    | ---- | ---------------------- |
    | a    | 光标后插入             |
    | i    | 光标所在位置插入       |
    | o    | 光标所在位置下一行插入 |