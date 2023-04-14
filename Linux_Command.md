<!--

 * @Author          : ZheZhang
 * @CreateDate      : 2023-03-22 14:46:23
 * @LastEditors     : ZhangBetter
 * @LastEditorsEmail: zhangzhenumberone@gmail.com
 * @LastEditTime    : 2023-04-14 10:58:31
 * @Description     : 著作权保护，转载请注明出处！
 * Copyright (c) 2023 by ZhangBetter Email: zhangzhenumberone@gmail.com, All Rights Reserved.
-->

# 关于Linux常用命令

> **本篇笔记主要记录Linux系统下的常用命令**  
* [关于Linux常用命令](#关于linux常用命令)
  * [yum、apt-get、curl、wget和pip的使用](#yumapt-getcurlwget和pip的使用)
  * [vim 常用命令](#vim-常用命令)

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
## vim 常用命令
> vim 可能需要手动安装：`yum install vim`  
> 本部分记录 vim 编辑器常用技巧和命令。  
> vim 存在三种模式：  
> 1. 命令模式：在该模式下是不能对文件直接编辑，可以输入快捷键进行一些操作（删除行，复制行，移动光标，粘贴等）  
> 2. 编辑模式：在该模式下可以对文件的内容进行编辑  
> 3. 末行模式：可以在末行输入命令对文件进行操作（搜索、替换、保存、退出、撤销、高亮）  

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
        :set autoindent         #设置缩进方式
        :set shiftwidth=4       #设置自动缩进长度
        ```

4. Tab 制表符设置  
`:set tabstop=4`  

5. 插入设置  
    | 命令 | 操作                   |
    | ---- | :--------------------- |
    | a    | 光标后插入             |
    | i    | 光标所在位置插入       |
    | o    | 光标所在位置下一行插入 |
    | Esc  | 进入命令模式           |
    | :    | 进入行命令模式         |

6. 光标移动  

    > 在移动光标的时候可以在快捷键前加上数字，例如 5h 表示光标向左移动5个单位。  

    | 快捷键 |       操作       |
    | :----: | :----------: |
    | H      | 左移 |
    | L      | 右移     |
    | J      | 下移 |
    | K      | 上移 |
    | ^      | 行首 |
    | $      | 行尾 |
    | GG     | 文件尾 |
    | gg  | 文件头 |
    | W      | 下一个单词 |
    | B      | 前一个单词 |
    | Ctrl+f | 朝向文件尾翻一页 |
    | Ctrl+b | 朝向文件头翻一页 |

7. 删除，复制，粘贴  

    | 命令 |                             操作                             |
    | :--: | :----------------------------------------------------------: |
    |  x   |                    删除光标所在位置的字符                    |
    |  dd  |                        删除光标所在行                        |
    |  D   |              删除光标所在位置到文件尾所有的字符              |
    |  d   | 普遍意义上的删除命令，和移动命令配合使用。例如dw表示删除光标所在位置到下一个单词词头之间的所有字符 |
    |  yy  |                        复制光标所在行                        |
    |  y   | 普遍意义上的复制命令，和移动命令配合使用。例如yw表示赋值光标所在位置到下一个单词词头之间的所有字符 |
    |  P   |            在光标所在位置粘贴最近复制/删除的内容             |

8. 撤销，重做

    |  命令  | 操作 |
    | :----: | :--: |
    |   u    | 撤销 |
    | Ctrl+R | 重做 |

9. 搜索，替换

    | 命令                                     | 操作                     |
    | ---------------------------------------- | ------------------------ |
    | :/string                                 | 向文件尾搜索字符串string |
    | :?string                                 | 向文件头搜索字符串string |
    | :[range]s/str_0/str_1  例如 –> :1,5s/a/b | 替换str_0为str_1         |

    

10. 保存，退出

    | 命令        | 操作           |
    | ----------- | -------------- |
    | :w          | 保存           |
    | :w filename | 另存为filename |
    | :q          | 退出           |
    | :q!         | 强制不保存退出 |
    | :wq!        | 强制保存并退出 |

    
