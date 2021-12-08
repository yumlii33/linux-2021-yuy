# Linux 命令行使用基础

## asciicema 使用

* 安装

* 

## vimtutor 练习记录

[lession 1](https://asciinema.org/a/KsoLl8GSayVT9MZq0QzUWgWpK)

[lession 2](https://asciinema.org/a/V62RGoqE94njq7CO4C0fsSZ5H)

[lession 3](https://asciinema.org/a/vJzNivDONlRg9J87pSpxlCtAz)

[lession 4](https://asciinema.org/a/PrRg17T0Drry9wV5CH7cBxZWc)

[lession 5](https://asciinema.org/a/eBUpydeHGP7qdCvANlq6miCia)

[lession 6](https://asciinema.org/a/03uU4u9e5bwL9CWPqiGLNj5FH)

[lession 7](https://asciinema.org/a/cL6SVAMSsV6nyry4mqhEXtcUj)


## vimtutor 完成后的自查清单

* 你了解vim有哪几种工作模式？

* Normal模式下，从当前行开始，一次向下移动光标10行的操作方法？如何快速移动到文件开始行和结束行？如何快速跳转到文件中的第N行？

    一次向下移动光标10行：`+10`+`<ENTER>` 

    快速移动到文件开始行：`gg` 或者 `1` + `G`

    快速移动到文件结束行： `G`

    如何快速跳转到文件中的第N行：`:N` + `<ENTER>` 或者 `N` + `G`

* Normal模式下，如何删除单个字符、单个单词、从当前光标位置一直删除到行尾、单行、当前行开始向下数N行？

    删除单个字符：`x`

    删除单个单词：`dw` 或者 `d1w`

    从当前光标位置一直删除到行尾：`d$`

    删除单行：`dd`

    删除当前行开始向下数N行：`Ndd`

* 如何在vim中快速插入N个空行？如何在vim中快速输入80个-？

    * 在vim中快速插入N个空行：
        `N`+`o`+`<ESC>`
        或者
        `N`+`O`+`<ESC>`

    * 在vim中快速输入80个-：
        `80`+`i`+`<ESC>`
        或者
        `80`+`a`+`<ESC>`

* 如何撤销最近一次编辑操作？如何重做最近一次被撤销的操作？

    撤销最近一次编辑操作：`u`

    撤销最近一次被撤销的操作：`CTRL-R` (keeping CTRL key pressed while hitting R)

* vim中如何实现剪切粘贴单个字符？单个单词？单行？如何实现相似的复制粘贴操作呢？

    * 剪切粘贴单个字符： `x` + `p`

    * 剪切粘贴单个单词： `dw` + `p`

    * 剪切粘贴单行： `dd` + `p`

    * 复制粘贴单个字符：
        把光标放到待复制的字符前，按下 `vy`
        把光标移动到待粘贴的位置，按下 `p`
        或者
        把光标放到待复制的字符前，按下 `yl`
        把光标移动到待粘贴的位置，按下 `p`   
        或者
        把光标放到待复制的字符后，按下 `yh`
        把光标移动到待粘贴的位置，按下 `p`   

    * 复制粘贴单个单词：
        把光标放在待复制的单词前,按下 `vey`   
        把光标移动到待粘贴的位置，按下 `p`
        或者
        把光标放在待复制的单词前,按下 `yw`   
        把光标移动到待粘贴的位置，按下 `p`

    * 复制粘贴单行：
        把光标放在待复制的行的行首，按下 `v$y`   
        把光标移动到待粘贴的位置，按下 `p`

* 为了编辑一段文本你能想到哪几种操作方式（按键序列）？

    * 行后附加内容：
        `A`
        输入内容
        `<ESC>`
    
    * 删除内容：
        删除行：`dd`
        删除单词：`dw`
    
    * 修改错误单词：
        跳转到要修改的位置，`j/k/h/l/w`
        `ce`
        输入正确的
        `<ESC>`
        
        

* 查看当前正在编辑的文件名的方法？查看当前光标所在行的行号的方法？

    查看当前正在编辑的文件名的方法：`CTRL-g`

    查看当前光标所在行的行号的方法：`CTRL-g`

* 在文件中进行关键词搜索你会哪些方法？如何设置忽略大小写的情况下进行匹配搜索？如何将匹配的搜索结果进行高亮显示？如何对匹配到的关键词进行批量替换？

    * 在文件中进行关键词搜索：  
        例如查找单词`error`:  
        `?`+`error`+`<ENTER>`  
        `/`+`error`+`<ENTER>`
        
    * 设置忽略大小写的情况下进行匹配搜索：
        设置`Ignore case`模式：`set:ic`+`<ENTER>`
        查找：`/`+`error`+`<ENTER>`
        取消`Ignore case`模式：`set:noic`+`<ENTER>`
        

    * 将匹配的搜索结果进行高亮显示：
        设置`hlsearch`和`incsearch`模式：`:set:hls is`+`<ENTER>`
        查找：`/`+`error`+`<ENTER>`
        取消`hlsearch`模式：`set:nohlsearch`+`<ENTER>`
        取消`incsearch`模式：`set:noincsearch`+`<ENTER>`

    * 对匹配到的关键词进行批量替换：
        To substitute new for the first old in a line type    `:s/old/new`
        To substitute new for all 'old's on a line type       `:s/old/new/g`
        To substitute phrases between two line #'s type       `:#,#s/old/new/g`
        To substitute all occurrences in the file type        `:%s/old/new/g`
        To ask for confirmation each time add 'c'             `:%s/old/new/gc`


* 在文件中最近编辑过的位置来回快速跳转的方法？

    * `goes back` : `CTRL-O`
    * `goes forward` : `CTRL-I`

* 如何把光标定位到各种括号的匹配项？例如：找到(, [, or {对应匹配的),], or }

    首先将光标放到待匹配的括号处  
    然后按`%`  
    光标会跳转到原光标所在位置的括号对应匹配的括号  

* 在不退出vim的情况下执行一个外部程序的方法？
    
    `:!` + `extrtnal command` + `<ENTER>`

    例如[在不退出vim的情况下执行ls命令]：`!ls` + `<ENTER>`

* 如何使用vim的内置帮助系统来查询一个内置默认快捷键的使用方法？如何在两个不同的分屏窗口中移动光标？

    * 使用vim的内置帮助系统来查询一个内置默认快捷键的使用方法：`:help command`+`<ENTER>`

    * 在两个不同的分屏窗口中移动光标：`CTRL`+`W`

## 参考链接

* [How it works - asciinema](https://asciinema.org/docs/how-it-works)