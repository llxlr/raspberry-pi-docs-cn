# APT

管理安装，升级和删除软件的最简单方法是使用Debian中的APT（高级打包工具）。如果某个软件打包在Debian中并且可以在树莓派上的ARM架构上运行，那么它也应该在Raspbian中可用。

要安装或删除软件包，您需要`root`用户权限，因此您的用户必须位于`sudoers`中，或者您必须以`root`身份登录。阅读有关[users](docs/usage/users.md)和[root](docs/usage/root.md)的更多信息。

要安装新软件包或更新现有软件包，您需要互联网连接。

请注意，安装软件会占用SD卡上的磁盘空间，因此您应注意磁盘使用情况并使用适当大小的SD卡。

另请注意，在安装软件时会执行锁定，因此您不能同时安装多个软件包。

## 软件源

APT将树莓派上的软件源列表保存在`/etc/apt/sources.list`文件中。在安装软件之前，您应该使用`apt update`更新软件包列表：

```bash
sudo apt update
```

## 使用APT安装软件包

```bash
sudo apt install tree
```

键入此命令应通知用户软件包将占用多少磁盘空间，并要求确认软件包安装。 输入`Y`（或仅按`Enter`，因为是默认操作）将允许进行安装。可以通过在命令中添加`-y`标志来绕开它：

```bash
sudo apt install tree -y
```

安装该软件包使`tree`对用户可用。

## 使用已安装的软件包

tree是一个命令行工具，可直观显示当前目录的结构及其所有内容。

- 输入`tree`运行tree命令。 例如：

```bash
tree
..
├── hello.py
├── games
│   ├── asteroids.py
│   ├── pacman.py
│   ├── README.txt
│   └── tetris.py

```

- 输入`man tree`会给出包`tree`的手动输入。
- 输入`whereis tree`显示`tree`安装的地方：

```bash
tree: /usr/bin/tree
```

## 使用APT卸载软件包

### Remove

您可以使用`apt remove`卸载软件包：

```bash
sudo apt remove tree
```

提示用户确认删除。同样，`-y`标志将自动确认。

### Purge

您还可以选择使用`apt purge`完全删除软件包及其相关的配置文件：

```bash
sudo apt purge tree
```

## 升级现有软件

如果有可用的软件更新，则可以通过`sudo apt update`获得更新，并通过`sudo apt upgrade`安装更新，这将升级所有软件包。要升级特定软件包，而不同时升级所有其他过时的软件包，可以使用`sudo apt install somepackage`（如果磁盘空间不足或下载带宽有限，这可能很有用。

## 搜索软件

您可以使用`apt-cache search`在档案库中搜索具有给定关键字的软件包：

```bash
apt-cache search locomotive
sl - Correct you if you type `sl' by mistake
```

您可以在使用`apt-cache show`安装它之前查看有关软件包的更多信息：

```bash
apt-cache show sl
Package: sl
Version: 3.03-17
Architecture: armhf
Maintainer: Hiroyuki Yamamoto <yama1066@gmail.com>
Installed-Size: 114
Depends: libc6 (>= 2.4), libncurses5 (>= 5.5-5~), libtinfo5
Homepage: http://www.tkl.iis.u-tokyo.ac.jp/~toyoda/index_e.html
Priority: optional
Section: games
Filename: pool/main/s/sl/sl_3.03-17_armhf.deb
Size: 26246
SHA256: 42dea9d7c618af8fe9f3c810b3d551102832bf217a5bcdba310f119f62117dfb
SHA1: b08039acccecd721fc3e6faf264fe59e56118e74
MD5sum: 450b21cc998dc9026313f72b4bd9807b
Description: Correct you if you type `sl' by mistake
 Sl is a program that can display animations aimed to correct you
 if you type 'sl' by mistake.
 SL stands for Steam Locomotive.
```
