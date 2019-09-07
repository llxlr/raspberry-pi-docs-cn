# SD卡

Raspberry Pi应该可以与任何兼容的SD卡一起使用，尽管应该遵循一些指导原则：

## SD卡大小（容量）

对于安装NOOBS或Raspbian的映像安装，建议的最小卡大小为8GB。对于Raspbian Lite图像安装，我们建议至少4GB。一些发行版，特别是LibreELEC和Arch，可以在更小的卡上运行。如果您计划在NOOBS中使用64GB或更高的卡，请先参阅[本页](sdxc_formatting.md)。

## SD卡类型

卡的类型确定卡的持续写入速度;一个4级卡可以4MB / s写入，而10级应该能够达到10MB/s。然而，应该注意的是，这并不意味着10级卡的性能优于普通使用的4级卡，因为通常这种写入速度是以读取速度和增加的寻道时间为代价来实现的。

## SD卡物理尺寸

最初的Raspberry Pi Model A和Raspberry Pi Model B需要全尺寸SD卡，新的[Raspberry Pi Model A+](https://www.raspberrypi.org/products/raspberry-pi-1-model/), [Raspberry Pi Model B+](https://www.raspberrypi.org/products/raspberry-pi-1-model-b/), [Raspberry Pi 2 Model B](https://www.raspberrypi.org/products/raspberry-pi-2-model-b/), [Raspberry Pi Zero](https://www.raspberrypi.org/products/raspberry-pi-zero/), and [Raspberry Pi 3 Model B](https://www.raspberrypi.org/products/raspberry-pi-3-model-b/)需要micro SD卡。

## 故障排除

我们建议您购买[此处](https://shop.pimoroni.com/products/noobs-8gb-sd-card)以及其他零售商提供的Raspberry Pi SD卡。这是一款8GB 6类SD卡（带有全尺寸SD适配器），性能优于市场上几乎所有其他SD卡，是一款物超所值的解决方案。

如果您的SD卡损坏有问题，请确保按照以下步骤操作：

1.确保使用的是正版SD卡。有许多便宜的SD卡可用，实际上比宣传的小，或者不会持续很长时间。
2.确保使用优质电源。您可以通过测量Raspberry Pi上TP1和TP2之间的电压来检查电源。如果在执行复杂任务时降至4.75V以下，则很可能不合适。
3.确保使用优质USB电缆作为电源。使用较低质量的电源时，TP1-> TP2电压可降至4.75V以下。这通常是由于USB电源线中的电线的阻力;为了省钱，USB电缆尽可能少地使用铜线，并且在电缆长度上可能损失1V（或1W）。
4.最后，如果你对Pi进行超频，就会发生corruption现象。此问题以前已得到解决，但使用的解决方法可能意味着它仍然可能发生。如果在检查上述步骤后仍然存在corruption问题，请告知我们。
