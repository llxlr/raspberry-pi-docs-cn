# .bashrc 和 .bash_aliases

在主文件夹中，您将找到一个名为`.bashrc`的隐藏文件，其中包含一些用户配置选项。您可以编辑此文件以满足您的需要。下次打开终端时，将对该文件中的更改进行操作，因为那是在读取`.bashrc`文件时进行的操作。

如果您希望在当前终端中进行更改，则可以使用`source 〜/.bashrc`或`exec bash`。它们实际上做的事情略有不同：前者只是重新执行`.bashrc`文件，这可能导致对路径之类的东西的不良更改，后者会用新的bash shell替换当前的shell，从而将shell重置为登录时的状态，丢弃您可能设置的所有shell变量。选择最合适的一个。

为您提供了一些有用的适应方法；其中一些默认情况下以“＃”注释掉。要启用它们，请删除＃，它们将在您下次启动树莓派或启动新终端时激活。

例如，一些`ls`别名：

```
alias ls='ls --color=auto'
#alias dir='dir --color=auto'
#alias vdir='vdir --color=auto'

alias grep='grep --color=auto'
alias fgrep='fgrep --color=auto'
alias egrep='egrep --color=auto'
```

提供此类别名是为了帮助其他系统（如Microsoft Windows）的用户使用（dir是DOS/Windows的ls）。其他的默认情况下是为ls和grep之类的命令的输出添加颜色。

还提供`ls`的更多变体：

```
# some more ls aliases
#alias ll='ls -l'
#alias la='ls -A'
#alias l='ls -CF'
```

Ubuntu用户可能对此很熟悉，因为该发行版默认提供它们。取消注释这些行，以便将来可以访问这些别名。

`.bashrc`也包含对`.bash_aliases`文件的引用，该文件默认情况下不存在。您可以添加它，以提供一种方便的方式将所有别名保存在单独的文件中。

```
if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi
```

这里的if语句在包含文件之前先检查文件是否存在。

然后，您只需创建文件`.bash_aliases`，并添加更多别名，如下所示：

```
alias gs='git status'
```

您可以将其他内容直接添加到此文件中，也可以添加到其他文件中，并包含该文件，例如上面的`.bash_aliases`示例。
