# 内核

树莓派的内核存储在GitHub中，可以在[github.com/raspberrypi/linux](https://github.com/raspberrypi/linux）上查看；它紧随主要的[Linux内核](https://github.com/torvalds/linux)之后。

Linux主内核正在不断更新。我们采用了在首页上提到的内核的长期发行版，并将所做的更改集成到树莓派内核中。然后，我们创建一个“下一步”分支，其中包含内核的不稳定端口。经过广泛的测试和讨论，我们将其推送到主分支。

- [更新内核](docs/linux/kernel/updating.md)
- [构建一个新内核](docs/linux/kernel/building.md)
- [配置内核](docs/linux/kernel/configuring.md)
- [将补丁应用到内核](docs/linux/kernel/patching.md)
- [获取内核头文件](docs/linux/kernel/headers.md)

## 将代码放入内核

您可能有很多原因想要将某些内容放入内核：

- 您已经编写了一些特定于树莓派的代码，希望每个人都能从中受益
- 您已经为设备编写了通用的Linux内核驱动程序，并希望每个人都可以使用它
- 您已修复通用内核错误
- 您已修复树莓派特定的内核错误

最初，您应该派生Linux存储库，并将其克隆到构建系统上。它既可以在树莓派上，也可以在用于交叉编译的Linux机器上。然后，您可以进行更改，测试它们并将其提交到fork中。

接下来，根据代码是否特定于树莓派：

- 对于特定于树莓派的更改或错误修复，请向内核提交请求请求。

- 对于一般的Linux内核更改（即新的驱动程序），需要先向上游提交这些更改。将它们提交到上游并被接受后，提交拉取请求，我们将收到请求。
