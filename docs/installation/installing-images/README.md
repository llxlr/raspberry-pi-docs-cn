# 安装操作系统镜像

此资源说明如何在SD卡上安装Raspberry Pi操作系统映像。您将需要另一台带有SD读卡器的计算机来安装映像。

我们建议大多数用户下载[NOOBS](../noobs.md)，它的设计非常易于使用。但是，希望安装特定映像的更高级用户应使用本指南。

## 下载镜像

推荐操作系统的官方镜像可从Raspberry Pi网站下载[Downloads page](https://www.raspberrypi.org/downloads/).

可从第三方供应商处获得替代分发。

如果您没有使用Etcher（见下文），则需要解压缩`.zip`下载以获取要写入SD卡的图像文件（`.img`）。

**注意**：ZIP存档中包含的Raspberry Pi桌面映像的Raspbian大小超过4GB，并使用[ZIP64](https://en.wikipedia.org/wiki/Zip_(file_format))格式。要解压缩存档，需要一个支持ZIP64的解压缩工具。以下zip工具支持ZIP64：

- [7-Zip](http://www.7-zip.org/) (Windows)
- [The Unarchiver](http://unarchiver.c3.cx/unarchiver) (Mac)
- [Unzip](http://www.info-zip.org/mans/unzip.html) (Linux)

## 将镜像写入SD卡

在开始之前，不要忘记检查[SD卡要求](../sd-cards.md).

您需要使用镜像烧录工具来安装已下载到SD卡上的图像。

**Etcher**是一种图形化SD卡写入工具，适用于Mac OS，Linux和Windows，是大多数用户最简单的选择。 Etcher还支持直接从zip文件中写入图像，无需任何解压缩。用Etcher烧录镜像：

- 下载 [Etcher](https://etcher.io/) and install it.
- 将SD卡读卡器与SD卡连接在一起。
- 打开Etcher并从硬盘驱动器中选择要写入SD卡的`.img`或`.zip`文件。
- 选择要写入镜像的SD卡。
- 检查您的选择，然后点击“Flash！”开始将数据写入SD卡。

有关此过程的更高级控制，请参阅我们的系统特定指南：

- [Linux](linux.md)
- [Mac OS](mac.md)
- [Windows](windows.md)
