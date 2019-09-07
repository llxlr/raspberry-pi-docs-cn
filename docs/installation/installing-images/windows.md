# 在Windows上安装操作系统镜像

[Etcher](https://etcher.io/)通常是大多数用户将图像写入SD卡的最简单选项，因此它是一个很好的起点。如果您在Windows上寻找替代方案，可以使用Win32DiskImager。

## Etcher

- 下载Windows安装包从[etcher.io](https://etcher.io/)
- 运行Etcher，选择解压缩的Raspbian镜像文件
- 选择SD卡
- 最后，单击** Burn **将Raspbian图像写入SD卡
- 你会看到一个进度条，完成后，该实用程序将自动卸载SD卡，以便可以安全地将其从计算机中删除。

## Win32DiskImager

- 将SD卡插入SD卡读卡器。如果您有一个SD卡插槽或USB端口中的SD适配器，则可以使用它。请注意分配给SD卡的驱动器号。您可以在Windows资源管理器的左侧栏中看到驱动器号，例如** G：**
- 从[Sourceforge项目页面](http://sourceforge.net/projects/win32diskimager/)下载Win32DiskImager实用程序作为安装程序文件，并运行它以安装该软件。
- 从桌面或菜单运行`Win32DiskImager`实用程序。
- 选择您之前提取的图像文件。
- 在设备框中，选择SD卡的驱动器号。小心选择正确的驱动器：如果选择了错误的驱动器，则可能会破坏计算机硬盘上的数据！如果您在计算机中使用SD卡插槽，并且无法在Win32DiskImager窗口中看到该驱动器，请尝试使用外部SD适配器。
- 单击“写入”并等待写入完成。
- 退出成像仪并弹出SD卡。

---

*本文使用来自eLinux wiki页面[RPi_Easy_SD_Card_Setup](http://elinux.org/RPi_Easy_SD_Card_Setup)的内容，该内容在[知识共享署名 - 相同方式共享3.0 Unported许可]下共享(http://creativecommons.org/licenses /by-sa/3.0/)*
