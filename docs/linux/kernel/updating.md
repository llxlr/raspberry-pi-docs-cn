# 更新内核

如果您使用标准的Raspbian更新/升级过程（请在[此处](docs/raspbian/updating.md)找到），这将自动将内核更新为最新的稳定版本。这是推荐的步骤。但是，在某些情况下，您可能希望更新到最新的`bleeding edge`或测试内核。

### 使用rpi-update进行手动更新

`rpi-update`实用程序将下载最新的（不稳定的，正在测试的）内核版本，并将所有必需的文件复制到您的系统上。注意，不能保证`rpi-update`中的最新内核能够正常工作！确保它与您的分发软件包不冲突。它没有提供自动卸载文件的方法。

升级内核后，您必须重新启动树莓派才能切换到更新的版本。

如果您使用的是已编译的内核，则`rpi-update`将覆盖它，并且您需要[rebuild](docs/linux/kernel/building.md)并重新安装内核。

自定义[configuration](docs/linux/kernel/configuring.md)通常可以在次要内核更新之间进行复制，但是使用`diff`实用工具查看更改内容并在新配置上重复更改更为安全。

### 恢复到当前的Raspbian内核

树莓派基础内核是`raspberrypi-kernel`软件包的一部分，而`bootloader`文件是`raspberrypi-bootloader`软件包的一部分。要在尝试`rpi-update`或自定义内核后恢复到当前的现有Raspbian内核，您需要通过运行以下命令来重新安装这两个软件包：

```bash
sudo apt-get install --reinstall raspberrypi-bootloader raspberrypi-kernel
```
