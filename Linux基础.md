# Linux基础

    CentOS 自动登录ROOT
    /etc/gdm/custom.conf
    deamon选项加入
    AutomaticLoginEnable=true
    AutomaticLogin=ROOT

    识别当前用户是否是管理员账号，使用用户的UID判断，uid为0为管理员
    centos6普通用户的uid从500开始
    centos7普通用户的uid从1000开始

    显示当前终端的命令
        tty

    终端：
        tty
        pty
        pts

    交互式接口
        GUI
        CLI

    显示当前系统版本
        cat /etc/centos-release
        lsb_release

    显示当前系统内核版本
        uname -r

    显示当前的系统CPU型号
        lscpu

    显示当前系统内存使用情况
        cat /proc/meminfo
        free

    显示网卡的工作速率
        mii-tool IFNAME

    显示当前登录的用户
        whoami

    显示当系统有谁在登录
        who
        w

    shell是linux系统与用户之间的接口

    显示当前系统所有的shell
        cat /etc/shells

    创建新文件
        > FILE

    退出当前shell
        logout
        ctrl+d

    常用的快捷键
        ctrl+l，清屏
        ctrl+a，光标跳到命令行首
        ctrl+e，光标条到命令行尾
        ctrl+k，删除光标处至命令尾的内容
        ctrl+u，删除光标处至命令首的内容
        ctrl+c，中断当前命令的执行

    显示当前系统的主机名
        hostname

    显示当前系统的登录提示符变量
        echo $PS1

    内部命令
        bash shell内置的命令，优先执行
    外部命令
        在磁盘可以找到的可执行的文件

    管理内部命令
        enable
            -n，禁用

    显示命令
        echo

    显示已缓存的命令
        hash

    缓存：将刚用的数据放在内存中，下次用此数据，不需要从硬盘上找，直接从内存取出

    命令执行的查找顺序
        别名 -- 内部 -- hash表 -- $PATH

    命令别名：
        alias

    命令的格式
        command [option...] [argument...]
            [option]
                短选项
                长选项

    多条命令顺序执行；
    一条长命令可以用\分割执行

    时钟
        硬件时间
            hwclock
                -w，以系统时间为准，将系统时间覆盖至硬件时间
                -s，以硬件时间为准，将系统时间覆盖至系统时间
        系统时间
            date MMDDHHmmYYYY.ss

    时区
        timedatectl set-timezone
        timedatectl list-timezones
        cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

    关机
        halt，poweroff
        shutdown
            TIME
            -r，重启
            -h，关机
            -c，取消关机操作

    screen
        创建新的screen会话
            screen -S [SESSION]
        加入会话screen会话
            screen -X [SESSION]
        剥离当前会话
            ctrl+a，d
        恢复会话
            screen -r

## 命令执行顺序：
    别名alias---内部命令---HASH---外部命令($PATH)
    可用type查看命令
    别名alias定义在 /当前用户/.bashrc文件   全局 /etc/.bashrc
    /etc/profile.d/  定义PS1（控制台显示格式）  env.sh(自定义)
    help查看内部命令帮助  man 

## echo
        ''强引用，变量不会替换
        ""弱引用，变量会替换
        ``反向单引号（$()等同），命令变量都识别
        -E 默认 不支持\解释功能
        -n 不换行
        -e  支持\解释功能
            "\a"  发出警告声
            "\b"  退格键
            "\c"  最后不加上换行符号
            "\n"  换行且光标移至行首
            "\r"  回车，即光标移至行首，但不换行
            "\t"  插入TAB
            "\\"  插入\
            "\0nnn" nnn为8进制，显示nnn的字符(ascii)
            "\xHH"  HH为16进制，显示HH的字符(ascii)
            {0..10}.{xxx,yyy}  等等

## history
             N 显示最近几条 
            -c 清除所有历史记录
            -d N 删除第N条历史记录
            -a 把内存history写入文件
            -r 把history文件写入内存
            -w 文件名 把history写入指定文件 不加参数默认
            -n 读history文件未读取的命令进内存
            -p 执行命令不保存历史
            -s 命令写入history 不执行
        HISTSIZE(保存多少条历史命令) 可/etc/profile文件修改
        HISTFILE 指定历史文件，默认 ~/.bash_history
        HISTFILESIZE:命令历史文件记录历史的条数
        HISTTIMEFORMAT="%F %T " 显示时间
        HISTIGNORE="str1:str2*... "忽略str1,str2开头的命令
        HISTCONTROL   ignoredups 默认，忽略重复的命令(连续)
                      ignorspace 忽略所有以空白开头的命令
                      ignoreboth 前两种组合
                      erasedups  删除重复命令(所有)
        存放文件在  /etc/procfile(全局) 或~/.bash_profile(用户)
            ！命令历史编号    直接执行此编号命令
            !!前一条命令
            !-1 -2  倒数第几条命令
            !:0   执行前一条命令，去除参数选项
            !.string   重复以string 开头的命令(最近一条)
            !?string   同上 包含
            !string:p   显示不执行
            !$:p       打印前一个命令最后参数   ll !$
            !*:p       打印前一个命令所有参数   ll !*
            ^string    删除前一个命令参数某字符
            ^string^string  同上替换
            !:gs/string/string 替换所有
            ctrl+r 搜索命令   ctrl+g 退出
            !&   前一条命令参数  = ESC松手+.  =ALT+.

## BASH快捷键

     Ctrl + l 清屏，相当于clear命令
     Ctrl + o 执行当前命令，并重新显示本命令 
     Ctrl + s 阻止屏幕输出，锁定 
     Ctrl + q 允许屏幕输出 
     Ctrl + c 终止命令 
     Ctrl + z 挂起命令

/etc/issue 登录前提示字符

## man帮助
    帮助手册中的段落说明：  
    NAME  名称及简要说明  
    SYNOPSIS 用法格式说明 
    • [] 可选内容 
    • <> 必选内容 
    • a|b 二选一 
    • { } 分组 
    • ... 同一内容可出现多次  
    DESCRIPTION 详细说明  
    OPTIONS  选项说明  
    EXAMPLES 示例  
    FILES  相关文件  
    AUTHOR 作者  
    COPYRIGHT 版本信息  
    REPORTING BUGS bug信息  
    SEE ALSO 其它帮助参考

    查看man手册页 
    man  [章节]  keyword 
    列出所有帮助 
    man –a keyword 
    搜索man手册 
    man -k keyword 列出所有匹配的页面 
    使用 whatis 数据库 
    相当于whatis 
    man –f keyword 
    打印man帮助文件的路径 
    man –w  [章节] keywor

    man命令的操作方法：使用less命令实现 
    space, ^v, ^f, ^F: 向文件尾翻屏 
    b, ^b: 向文件首部翻屏 
    d, ^d: 向文件尾部翻半屏 
    u, ^u: 向文件首部翻半屏 
    RETURN, ^N, e, ^E or j or ^J: 向文件尾部翻一行 y or ^Y or ^P or k or ^K：向文件首部翻一行 
    q: 退出 #：跳转至第#行 
    1G: 回到文件首部 
    G：翻至文件尾部

    man搜索
    /KEYWORD: 
    以KEYWORD指定的字符串为关键字，从当前位置向文件尾部搜索；不区 分字符大小写； 
    n: 下一个 
    N：上一个 
    ?KEYWORD: 
    以KEYWORD指定的字符串为关键字，从当前位置向文件首部搜索；不区 分字符大小写； 
    n: 跟搜索命令同方向，下一个 
    N：跟搜索命令反方向，上一个
