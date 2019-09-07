# 格式化一张SDXC卡以便安装NOOBS

关于[SD卡规格](https://www.sdcard.org/developers/overview/capacity/)，任何大于32GB的SD卡都是SDXC卡，必须使用exFAT文件系统进行格式化。这意味着官方SD Formatter工具将*总是*格式化64GB或更大的卡作为exFAT。

Raspberry Pi的引导加载程序内置于GPU中且不可更新，仅支持从FAT文件系统（FAT16和FAT32）读取，并且无法从exFAT文件系统启动。因此，如果要在64GB或更大的卡上使用NOOBS，则需要先将其重新格式化为FAT32，然后再将NOOBS文件复制到其中。

## Linux和Mac OS

这些操作系统内置的标准格式化工具可以创建FAT32分区;它们也可能被标记为FAT或MS-DOS。在继续执行[NOOBS指令](noobs.md)的其余部分之前，只需删除现有的exFAT分区并创建并格式化新的FAT32主分区。在Mac上，这意味着使用内置的“磁盘工具”应用程序。

## Windows

Windows中内置的标准格式化工具是有限的，因为它们只允许最大32GB的分区格式化为FAT32，因此要将64GB分区格式化为FAT32，您需要使用第三方格式化工具。一个简单的工具是[FAT32格式](http://www.ridgecrop.demon.co.uk/guiformat.htm)，它作为名为`guiformat.exe`的单个文件下载 - 无需安装。

首先运行[SD Formatter](https://www.sdcard.org/downloads/formatter_4/)工具，确保删除SD卡上的任何其他分区。然后运行FAT32格式(guiformat.exe)工具，确保选择正确的驱动器号，将其他选项保留为默认设置，然后单击“开始”。完成后，您可以继续执行[NOOBS指令](noobs.md)的其余部分。

如果FAT32格式工具不适合您，则可以选择[MiniTool分区向导免费版](http://www.minitool.com/partition-manager/partition-wizard-home.html)和[EaseUS Partition Master免费版](http://www.easeus.com/partition-manager/epm-free.html)是全功能分区编辑器工具的“家庭用户”版本，因此不能直接使用。
