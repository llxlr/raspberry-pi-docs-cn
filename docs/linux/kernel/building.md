# 内核构建

构建内核有两种主要方法。您可以在树莓派上本地构建，这将需要很长时间。或者您可以交叉编译，这更快，但需要更多设置。

## 本地构建

在树莓派上，首先安装[Raspbian](https://www.raspberrypi.org/downloads/)的最新版本。然后启动您的树莓派，插入以太网以访问源，然后登录。

首先安装Git和构建依赖项：

```bash
sudo apt-get install git bc bison flex libssl-dev
```

接下来获取源，这将需要一些时间：

```bash
git clone --depth=1 https://github.com/raspberrypi/linux
```

<a name="choosing_sources"></a>

### 选择源

上面的git clone命令将下载当前活动的分支（我们正在从中构建Raspbian映像的分支），而没有任何历史记录。省略`--depth = 1`将会下载整个存储库，包括所有分支的全部历史记录，但这会花费更长的时间并占用更多的存储空间。

要下载其他分支（同样没有历史记录），请使用`--branch`选项：

```bash
git clone --depth=1 --branch rpi-4.18.y https://github.com/raspberrypi/linux
```

有关可用分支的信息，请参考[原始GitHub存储库](https://github.com/raspberrypi/linux)。

### 内核配置

配置内核；以及默认配置，您可能希望[更详细地配置内核](docs/linux/kernel/configuring.md)或[从其他来源应用补丁](docs/linux/kernel/patching.md)，以添加或删除所需的功能：

运行以下命令，具体取决于您的树莓派版本。

### 树莓派 1，树莓派 Zero，树莓派 Zero W和计算模块的默认构建配置

```bash
cd linux
KERNEL=kernel
make bcmrpi_defconfig
```

### 树莓派 2，树莓派 3，树莓派 3+和计算模块3默认构建配置

```bash
git clone https://github.com/raspberrypi/tools ~/tools
```

更新`$ PATH`环境变量可使系统知道交叉编译所需的文件位置。在32位主机系统上，您可以使用以下命令进行更新和重新加载：

```bash
echo PATH=\$PATH:~/tools/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian/bin >> ~/.bashrc
source ~/.bashrc
```

如果您使用的是64位主机系统，则应使用：

```bash
echo PATH=\$PATH:~/tools/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian-x64/bin >> ~/.bashrc
source ~/.bashrc
```
### 获取资源

要下载当前分支的最小源代码树，请运行：

```bash
git clone --depth=1 https://github.com/raspberrypi/linux
```

有关如何选择其他分支的说明，请参见上面的[**选择源**](＃choosing_sources)。

### 构建资源

要构建用于交叉编译的源，请通过执行以下命令确保您对计算机具有所需的依赖关系：

```bash
sudo apt-get install git bison flex libssl-dev
```
如果您发现需要其他东西，请提交请求请求以更改文档。

输入以下命令来构建源文件和设备树文件：

对于树莓派 1，树莓派 Zero，树莓派 Zero W或计算模块：

```bash
cd linux
KERNEL=kernel
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- bcmrpi_defconfig
```

对于树莓派 2，树莓派 3，树莓派 3+或计算模块3：

```bash
cd linux
KERNEL=kernel7
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- bcm2709_defconfig
```

然后，对于两个：

```bash
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- zImage modules dtbs
```

**注意**: 为了加快在多处理器系统上的编译并在单处理器系统上获得一些改进，请使用`-j n`，其中n是处理器数*1.5。另外，您也可以尝试一下，看看有什么用！

### 直接安装到SD卡上

构建内核之后，您需要将其复制到树莓派上并安装模块。最好直接使用SD卡读卡器完成此操作。

首先，在插入SD卡之前和之后使用`lsblk`进行识别。 您应该以如下形式结束：

```
sdb
   sdb1
   sdb2
```

其中sdb1是FAT（引导）分区，而sdb2是ext4文件系统（根）分区。

如果是NOOBS卡，则应该看到以下内容：

```
sdb
  sdb1
  sdb2
  sdb5
  sdb6
  sdb7
```

其中sdb6是FAT（引导）分区，而sdb7是ext4文件系统（根）分区。

首先安装这些，并调整NOOBS卡的分区号：

```bash
mkdir mnt
mkdir mnt/fat32
mkdir mnt/ext4
sudo mount /dev/sdb1 mnt/fat32
sudo mount /dev/sdb2 mnt/ext4
```

接下来，安装模块：

```bash
sudo make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- INSTALL_MOD_PATH=mnt/ext4 modules_install
```

最后，将内核和设备树blob复制到SD卡上，确保备份旧内核：

```bash
sudo cp mnt/fat32/$KERNEL.img mnt/fat32/$KERNEL-backup.img
sudo cp arch/arm/boot/zImage mnt/fat32/$KERNEL.img
sudo cp arch/arm/boot/dts/*.dtb mnt/fat32/
sudo cp arch/arm/boot/dts/overlays/*.dtb* mnt/fat32/overlays/
sudo cp arch/arm/boot/dts/overlays/README mnt/fat32/overlays/
sudo umount mnt/fat32
sudo umount mnt/ext4
```

另一种选择是将内核复制到同一位置，但使用不同的文件名（例如，kernel-myconfig.img），而不是覆盖kernel.img文件。然后，您可以编辑config.txt文件以选择Pi引导进入的内核：

```
kernel=kernel-myconfig.img
```

这样做的好处是，可以使内核与系统和任何自动更新工具管理的内核映像分开，并允许您在内核无法启动的情况下轻松地恢复到普通内核。

最后，将卡插入树莓派并启动！
