# Linux

解释一些基本的Linux用法，以及绕过树莓派并管理其文件系统和用户的命令。

## 目录

- [文件系统](docs/linux/filesystem/)
    - [主文件夹](docs/linux/filesystem/home.md)
        - 你的用户在Pi上的主文件夹，您可以保存文件
    - [整个文件系统](docs/linux/filesystem/whole-filesystem.md)
        - 其余的Linux文件系统
    - [备用](docs/linux/filesystem/backup.md)
        - 备份文件和操作系统映像
- [用法](docs/linux/usage/)
    - [命令](docs/linux/usage/commands.md)
        - 一些基本的和更高级的Linux命令
    - [文本编辑器](docs/linux/usage/text-editors.md)
        - Pi上提供了一系列文本编辑器
    - [用户](docs/linux/usage/users.md)
        - 在Pi系统上设置多个Linux用户
    - [根用户](docs/linux/usage/root.md)
        - `root`用户和`sudo`前缀
    - [脚本](docs/linux/usage/scripting.md)
        - 组合命令以产生更复杂的动作
    - [Cron/Crontab](docs/linux/usage/cron.md)
        - 设置计划任务
    - [.bashrc和.bash_aliases](docs/linux/usage/bashrc.md)
        - 您的shell配置和别名
    - [systemd](docs/linux/usage/systemd.md)
        - 配置systemd服务以在引导时启动脚本
    - [rc.local](docs/linux/usage/rc-local.md)
        - 初始化的配置
- [软件](docs/linux/software/)
    - [APT](docs/linux/software/apt.md)
        - 用APT安装软件
    - [Python](docs/linux/software/python.md)
        - 使用Python包管理器安装软件，例如`pip`
    - [Ruby](docs/linux/software/ruby.md)
        - 使用Ruby的包管理器`ruby gems`安装软件
- [内核](docs/linux/kernel/)
    - [更新](docs/linux/kernel/updating.md)
        - 在Raspberry Pi上更新Linux内核
    - [建构](docs/linux/kernel/building.md)
        - 在Raspberry Pi上构建Linux内核
    - [配置](docs/linux/kernel/configuring.md)
        - 在Raspberry Pi上配置Linux内核
    - [修复](docs/linux/kernel/patching.md)
        - 在Raspberry Pi上将补丁应用于Linux内核
    - [头](docs/linux/kernel/headers.md)
        - 获取内核头文件
