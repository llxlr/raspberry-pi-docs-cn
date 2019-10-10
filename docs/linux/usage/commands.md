# Linux命令

以下是一些基本的和常见的Linux命令以及示例用法：

## 文件系统

### ls

`ls`命令列出当前目录（或指定的目录）的内容。它可以与`-l`标志一起使用，以列表格式显示有关每个文件和目录的其他信息（权限，所有者，组，大小，日期和上次编辑的时间戳）。`-a`标志可让您查看以`.`开头的文件（即dotfiles）（译者：也就是隐藏文件和文件夹）。

### cd

使用`cd`将当前目录更改为指定的目录。你可以使用相对路径（即`cd directoryA`）或绝对路径（即`cd /home/pi/directoryA`）。

### pwd

`pwd`命令显示当前工作目录的名称：在树莓派上，输入pwd将输出类似`/home/pi`的内容。

### mkdir

您可以使用`mkdir`创建一个新目录，例如`mkdir newDir`将在当前工作目录中创建目录`newDir`。

### rmdir

要删除空目录，使用`rmdir`。因此，例如，`rmdir oldDir`仅在目录为空时才会删除目录`oldDir`。

### rm

命令rm删除指定的文件（或与`-r`一起使用时从目录中递归删除）。使用此命令时要小心：以这种方式删除的文件基本上永远消失了！（译者：不要用`sudo rm -rf /*`，这一点都不好玩，因为会删掉所有文件，死的连渣都不剩，不要回复！不要回复！）

### cp

使用`cp`可以复制文件并将其放置在指定的位置（这类似于复制和粘贴）。例如，`cp 〜/fileA /home/otherUser/`会将文件`fileA`从您的主目录复制到用户`otherUser`的文件中（假设您有权在此处复制它）。此命令可以将`FILE FILE`（`cp fileA fileB`），`FILE DIR`（cp fileA /directoryB/`）或`-r DIR DIR`（递归地复制目录的内容）作为参数。

### mv

`mv`命令移动文件并将其放置在指定位置（因此，`cp`执行`复制粘贴`的作用，`mv`执行`剪切粘贴`的作用）。用法类似于`cp`。所以`mv 〜/fileA /home/otherUser/`会将文件`fileA`从您的主目录移动到用户`otherUser`的目录中。 该命令可以将`FILE FILE`（`mv fileA fileB`），`FILE DIR`（`mv fileA /directoryB/`）或`DIR DIR`（`mv /directoryB /directoryC`）作为参数。创建文件和目录后，此命令也可用作重命名文件和目录的方法。

### touch

命令`touch`设置指定文件的最后修改时间戳，如果尚不存在，则创建它。

### cat

您可以使用`cat`列出文件的内容，例如`cat thisFile`将显示`thisFile`的内容。可以用来列出多个文件的内容，即`cat *.txt`将列出当前目录中所有`.txt`文件的内容。

### head

`head`命令显示文件的开头。可以与`-n`一起使用以指定要显示的行数（默认为10），或与`-c`一起使用以指定字节数。

### tail

与`head`相反，`tail`显示文件的结尾。可以通过`-b`为512字节块指定文件的起点，为字节为`-c`表示行数，或者通过`-n`为行数指定文件的起点。

### chmod

通常，您可以使用`chmod`来更改文件的权限。chmod命令可以使用符号`u`（拥有文件的用户），`g`（文件组）和`o`（其他用户）以及权限`r`（读取），`w`（ 写）和`x`（执行）。 使用`chmod u+x *filename*`将为文件所有者添加执行权限。

### chown

`chown`命令更改拥有文件的用户或组。通常需要使用sudo以root身份运行。`sudo chown pi:root *filename*`会将所有者更改为`pi`，将组更改为`root`。

### ssh

ssh表示安全shell。使用加密的网络连接连接到另一台计算机。

有关更多详细信息，请参见[SSH（安全shell）](docs/remote-access/ssh/)

### scp

scp命令使用ssh将文件从一台计算机复制到另一台计算机。

有关更多详细信息，请参见[SCP（安全副本）](docs/remote-access/ssh/scp.md)

### sudo

`sudo`命令使您能够以超级用户或其他用户身份运行命令。将`sudo -s`用于超级用户shell。

有关更多详细信息，请参见[root用户/sudo](docs/linux/usage/root.md)

### dd

`dd`命令复制一个文件，将其转换为指定的文件。它通常用于将整个磁盘复制到单个文件或再次复制回来。因此，例如，`dd if=/dev/sdd of=backup.img`将从`/dev/sdd`的SD卡或USB磁盘驱动器创建备份映像。将映像复制到SD卡时，请确保使用正确的驱动器，因为它会覆盖整个磁盘。

### df

使用`df`显示已安装文件系统上可用和已使用的磁盘空间。使用`df -h`以人类可读的格式查看输出，使用M表示MB，而不显示字节数。

### unzip

`unzip`命令从压缩的`zip`文件中提取文件。

### tar

使用`tar`来存储或从磁带存档文件中提取文件。它也可以通过压缩类似于`zip`文件的文件来减少所需的空间。

要创建压缩文件，请使用`tar -cvzf *filename.tar.gz* *directory/*`

要提取文件的内容，请使用`tar -xvzf *filename.tar.gz*`

### pipes

管道允许一个命令的输出用作另一命令的输入。管道符号是垂直线`|`。例如，仅显示`ls`命令的前十个条目，可以通过`head`命令`ls | head`

### tree

使用`tree`命令显示目录以及缩进为树形结构的所有子目录和文件。

### &

使用`＆`在后台运行命令，释放shell程序以供将来使用。

### wget

使用`wget`从网上直接下载文件到计算机。因此`wget https://www.raspberrypi.org/documentation/linux/usage/commands.md`会将这个文件作为`commands.md`下载到您的计算机上。

### curl

使用`curl`将文件下载到服务器或从服务器上传文件。默认情况下，它将文件的文件内容输出到屏幕。

### man

显示带有`man`的文件的手册页。要了解更多信息，请运行`man man`以查看man命令的手册页。

## 搜索

### grep

使用`grep`在文件内部搜索某些搜索模式。例如，`grep "search" *.txt`将在当前目录中以`.txt`结尾的所有文件中查找字符串`search`。

`grep`命令支持正则表达式，该正则表达式允许在搜索中包含特殊的字母组合。

### awk

`awk`是一种编程语言，可用于搜索和处理文本文件。

### find

`find`命令在目录和子目录中搜索与某些模式匹配的文件。

### whereis

使用`whereis`查找命令的位置。它遍历标准程序位置，直到找到请求的命令。

## 联网

### ping

`ping`实用程序通常用于检查是否可以与其他主机进行通信。仅指定主机名（例如`ping raspberrypi.org`）或IP地址（例如`ping 8.8.8.8`）即可将其用于默认设置。它可以用`-c`标志指定要发送的数据包数量。

### nmap

`nmap`是一种网络探索和扫描工具。它可以返回有关主机或主机范围的端口和操作系统信息。仅运行`nmap`将显示可用选项以及用法示例。

### hostname

`hostname`命令显示系统的当前主机名。特权（超级）用户可以通过提供主机名作为参数来将其设置为新主机名（例如，`hostname new-host`）。

### ifconfig

如果运行时不带任何参数（例如，`ifconfig`），请使用`ifconfig`显示当前系统上接口的网络配置详细信息。通过为命令提供接口名称（例如`eth0`或`lo`），您可以更改配置：请查看手册页以获取更多详细信息。
