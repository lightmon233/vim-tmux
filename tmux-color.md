首先确保不在Tmux中以及在Tmux中Shell的环境变量TERM是相同的。
环境变量TERM的值一般是screen-256color或xterm-256color，我们把TERM变量统一成其中一个就行。
使用echo $TERM命令查看环境变量。下面以我的环境为例：

不在Tmux中，Shell执行echo $TERM返回xterm-256color，于是下一步就将Tmux的TERM设为xterm-256color。
（也可以将$TERM都统一为screen-256color，这样就需要先把Fish Shell的$TERM设为screen-256color，但是只有好像Vim都支持这两种，Neovim只支持xterm-256color）。

进入Tmux的配置文件~/.tmux.conf，设置以下命令：
```bash
set -g default-terminal "xterm-256color"  
#set -g default-terminal "screen-256color"   # 如果使用screen-256color则用这条指令
```
设置完后保存退出，并确保退出所有Tmux的session，重启Tmux，查看在Tmux中以及不在Tmux中Vim的颜色是否相同。如果还不相同，则看下一条。

开启Nvim和Tmux的TrueColor
如果颜色仍然不相同，有可能是一方使用TrueColor而另一方使用的是256color。由于目前主流的终端模拟器都支持TrueColor，因此这里就将Nvim和Tmux都设置为TrueColor。

a. 确保终端模拟器支持TrueColor

在这里 termstandard/colors 查看终端模拟器对TrueColor支持，如果您当前使用的终端不支持TrueColor，建议换成支持TrueColor的终端。

当然也可也使用24-bit-color.sh 脚本测试终端是否支持TrueColor。

在非Tmux下的Shell中运行脚本，如果终端支持TrueColor，则会显示如下：


如果终端不支持TrueColor，则显示会与下面的效果类似：


b. Tmux开启TrueColor

进入Tmux的配置文件~/.tmux.conf，设置以下命令：
```bash
set-option -ga terminal-overrides ",*256col*:Tc" 
```
设置完成后，重启Tmux，运行脚本24-bit-color.sh测试。

c. nvim开启TrueColor

在nvim配置文件~/.config/nvim/init.vim中设置
```bash
set termguicolors
```
这样就全部设置完成了，最后再看看Vim在Tmux中颜色是否改变。

参考：
为 vim + tmux 开启真彩色(true color)
————————————————
版权声明：本文为CSDN博主「Lkites」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_37151416/article/details/122917222
