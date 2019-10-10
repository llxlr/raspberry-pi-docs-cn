# 配置内核

Linux内核是高度可配置的。高级用户可能希望修改默认配置，以根据他们的需要对其进行自定义，例如启用新的或实验性的网络协议，或启用对新硬件的支持。

配置通常是通过`make menuconfig`界面完成的。另外，您可以手动修改`.config`文件，但是对于新用户而言，这可能会更加困难。

## 准备配置内核

`menuconfig`工具需要`ncurses`开发头文件才能正确编译。可以使用以下命令安装它们：

```bash
$ sudo apt-get install libncurses5-dev
```

您还需要下载并准备内核源代码，如[构建指南](docs/linux/kernel/building.md)中所述。特别是，请确保您已安装默认配置。

对于树莓派 1的所有型号（包括计算模块和树莓派 Zero）：

```bash
$ KERNEL=kernel
$ make bcmrpi_defconfig
```

如果您是交叉编译，则第二行应为：

```bash
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- bcmrpi_defconfig
```

对于树莓派 2/3的所有型号（包括树莓派 3+和计算模块3）：

```bash
$ KERNEL=kernel7
$ make bcm2709_defconfig
```

如果您是交叉编译，则第二行应为：

```bash
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- bcm2709_defconfig
```

## 使用menuconfig

一切准备就绪并准备就绪后，您可以按如下所示编译和运行`menuconfig`实用程序：

```bash
$ make menuconfig
```

如果您要交叉编译，请执行以下操作：

```bash
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- menuconfig
```

`menuconfig`实用程序具有简单的键盘导航。经过简短的编译，您将看到一个子菜单列表，其中包含可以配置的所有选项。有很多东西，所以花点时间通读它们并结识。

使用箭头键进行定位，使用Enter键进入子菜单（由`--->`表示），两次退出以进入级别或退出，并使用空格键循环显示选项的状态。有些选项有多个选择，在这种情况下，它们将显示为子菜单，而Enter键将选择一个选项。您可以在大多数条目上按`h`以获取有关该特定选项或菜单的帮助。

抵制尝试启用或禁用许多功能的诱惑；破坏配置相对容易，因此请从小处着手并熟悉配置和构建过程。


## 退出，保存和加载配置

完成所需的更改后，请按`Escape`，直到提示您保存新配置。默认情况下，这将保存到`.config`文件中。您可以通过复制该文件来保存和加载配置。
