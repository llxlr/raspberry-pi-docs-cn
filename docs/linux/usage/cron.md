# 使用Cron安排任务

Cron是在Unix系统上配置计划任务的工具。它用于计划命令或脚本以固定的间隔定期运行。任务范围从每天午夜备份用户的主文件夹到每小时记录CPU信息。

命令`crontab`（cron表）用于编辑正在运行的计划任务列表，并且是按用户完成的；每个用户（包括root）都有自己的crontab。

## Cron GUI

通过安装`gnome-schedule`软件包可以获得Cron的图形应用程序：

```bash
sudo apt-get install gnome-schedule
```

然后，您可以从主菜单启动程序`计划任务`。

## 编辑crontab

运行带有`-e`标志的`crontab`来编辑cron表：

```bash
crontab -e
```

### 选择编辑器

第一次运行`crontab`时，系统会提示您选择编辑器。如果不确定使用哪个，请按Enter键选择`nano`。

### 添加计划任务

Cron条目的布局由六个部分组成：分钟，小时，每月的某天，一年中的某月，一周中的某天以及要执行的命令。

```
# m h  dom mon dow   命令
```

```
# * * * * *  command to execute
# ┬ ┬ ┬ ┬ ┬
# │ │ │ │ │
# │ │ │ │ │
# │ │ │ │ └───── day of week (0 - 7) (0 to 6 are Sunday to Saturday, or use names; 7 is Sunday, the same as 0)
# │ │ │ └────────── month (1 - 12)
# │ │ └─────────────── day of month (1 - 31)
# │ └──────────────────── hour (0 - 23)
# └───────────────────────── min (0 - 59)
```

例如：

```
0 0 * * *  /home/pi/backup.sh
```

这个cron条目将每天在午夜运行`backup.sh`脚本。

### 查看预定的任务

使用以下命令查看当前保存的计划任务：

```bash
crontab -l
````

### 重启后运行任务

要在每次树莓派启动时运行命令，请输入`@reboot`而不是时间和日期。例如：

```bash
@reboot python /home/pi/myscript.py
```

每次树莓派重新启动时，这将运行您的Python脚本。如果您希望在树莓派继续启动时在后台运行命令，请在行末添加空格和`＆`，如下所示：

```bash
@reboot python /home/pi/myscript.py &
```
