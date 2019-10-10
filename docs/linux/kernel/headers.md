# 内核头

如果要编译内核模块或类似模块，则将需要Linux Kernel标头。这些提供了编译与内核接口的代码时所需的各种功能和结构定义。

如果您已从github克隆了整个内核，则标头已包含在源代码树中。如果不需要所有其他文件，则可以仅从Raspbian存储库中安装内核头文件。

```bash
sudo apt-get install raspberrypi-kernel-headers
```

请注意，此命令可能要花很长时间才能完成，因为它会安装许多小文件。没有进度指示器。

制作新的内核发行版时，您将需要与该内核版本匹配的标头。更新仓库以反映最新的内核版本可能需要花费几周的时间。如果发生这种情况，最好的方法是按照[Build Section](docs/linux/kernel/building.md)中的描述克隆内核。
