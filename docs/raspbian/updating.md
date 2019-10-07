# 更新和升级Raspbian

This section covers how to deploy software updates to devices running Raspbian.

Before we go any further, let's investigate why keeping our devices updated is important.

The first and probably the most important reason is security. A device running Raspbian contains millions lines of code that you rely on. Over time, these millions lines of code will expose well-known vulnerabilities known as [Common Vulnerabilities and Exposures (CVE)](https://cve.mitre.org/index.html), which are documented in publicly available databases meaning that they are easy to exploit. [Here is a example](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-8831) of a recent CVE found in KODI that provides a bit more insight on what information is available in the database and how CVEs are tracked. The only way to mitigate these exploits as a user of Raspbian is to keep your software up to date, as the upstream repositories track CVEs closely and try to mitigate them quickly.

The second reason, which is related to the first, is that the software you are running on your device most certainly contains bugs. Some bugs are CVEs, but bugs could also be affecting the desired functionality without being related to security. By keeping your software up to date, you are lowering the chances of hitting these bugs.

## APT (高级包管理工具)

你可以在终端使用 [apt](../linux/software/apt.md) 工具来更新Raspbian内的软件。从任务栏或程序菜单打开一个终端窗口：

![终端Terminal](../usage/terminal/images/terminal.png)

首先，通过回车运行以下命令 **更新** 你系统的包列表：

```bash
sudo apt-get update
```

然后，通过以下命令 **升级** 你安装的所有包到它们的最终版本：

```bash
sudo apt-get dist-upgrade
```

Generally speaking, doing this regularly will keep your installation up to date, in that it will be equivalent to the latest released image available from [raspberrypi.org/downloads](https://www.raspberrypi.org/downloads/).

However, there are occasional changes made in the Foundation's Raspbian image that require manual intervention, for example a newly introduced package. These are not installed with an upgrade, as this command only updates the packages you already have installed.

### 更新内核和固件

The kernel and firmware are installed as a Debian package, and so will also get updates when using the procedure above. These packages are updated infrequently and after extensive testing.

### 空间使用

When running `sudo apt-get dist-upgrade`, it will show how much data will be downloaded and how much space it will take up on the SD card. It's worth checking with `df -h` that you have enough free disk space, as unfortunately `apt` will not do this for you. Also be aware that downloaded package files (`.deb` files) are kept in `/var/cache/apt/archives`. You can remove these in order to free up space with `sudo apt-get clean`.

### 从Jessie升级到Stretch

升级一个已存在的 Jessie 镜像是可以的，但是不能保证在所有环境下都能工作。 如果你想尝试升级 Jessie 镜像到 Stretch，我们强烈推荐先做个备份 — 对于更新失败导致的数据丢失，我们不承担任何责任。

为了升级，首先修改 `/etc/apt/sources.list` 和 `/etc/apt/sources.list.d/raspi.list`文件。 在两个文件中， 把所有的 `jessie` 关键词改为 `stretch`。（这两个文件都需要使用sudo进行编辑）

打开终端窗口并执行：

```bash
sudo apt-get update
sudo apt-get -y dist-upgrade
```
对任何提示回答“yes”。 There may also be a point at which the install pauses while a page of information is shown on the screen – hold the <kbd>space</kbd> key to scroll through all of this and then press <kbd>q</kbd> to continue.

Finally, if you are not using PulseAudio for anything other than Bluetooth audio, remove it from the image by entering:

```
sudo apt-get -y purge "pulseaudio*"
```

如果转移到一个新的树莓派型号 （例如Raspberry Pi 3B+），你或许也需要使用以上说明来升级内核和固件。

## 第三方解决方案

本节介绍了为什么需要第三方解决方案和为什么 [apt](../linux/software/apt.md) 不是最佳解决方案。它还涵盖了支持Raspbian的现有第三方解决方案。

[Apt](../linux/software/apt.md) 是一个方便更新运行在你Raspbian设备软件的方式， 但是当你有较大数量的设备要更新时这个方法的限制变得很明显, and 特别是 when you do not have physical access to your devices and when 他们是地理分布。

If you lack physical access to your devices and want to deploy unattended updates Over-The-Air (OTA), here are some general requirements:

- Updating must not under any circumstances break (“brick”) the devices, e.g if the update is interrupted (power loss, network loss, etc.), the system should fall back to a working state
- Updating must be [atomic](https://en.wikipedia.org/wiki/Atomicity_(database_systems)): update succeeded or update failed; nothing in between that could result in a device still “functioning” but with undefined behavior
- Updating must be able to install images/packages that are cryptographically signed, preventing third parties from installing software on your device
- Updating must be able to install updates using an secure communication channel

Unfortunately [apt](../linux/software/apt.md) lacks the robustness features, i.e. atomicity and fall-back. This is why third-party solutions have started to appear that try to solve the problems that need to be addressed for deploying unattended updates OTA.

### Mender

Mender 是一个端到端的开源更新管理器。A robust update process is implemented with atomic dual system update, there is always one working system partition, and Mender updates the one that is not running. 你可以在 [Mender: how it works](https://mender.io/product/how-it-works) 网页阅读更多。

Mender 支持 Raspbian。 按照教程 [Raspbian with Mender](https://hub.mender.io/t/raspberry-pi-3-model-b-b-raspbian/140) 启用 Mender 在你 Raspbian 镜像上的支持。
