# Hello Teapot

这会显示一个旋转的茶壶，其视频剪辑来自`hello_video`纹理映射到其表面。真是令人印象深刻！如果您熟悉一款名为[Blender](https://en.wikipedia.org/wiki/Blender_(software))的软件，则可以识别茶壶模型。这同时演示了OpenGL ES渲染和视频解码/播放。

![Teapot](https://github.com/White-Album-Lab/raspberry-pi-docs-cn/blob/master/docs/usage/demos/images/teapot.jpg)

```bash
cd ..
cd hello_teapot
ls
```

注意到绿色的`.bin`文件了吗？ 好的，运行它！

```bash
./hello_teapot.bin
```

当您尝试运行此演示时，您可能会收到以下错误：

```bash
Note: ensure you have sufficient gpu_mem configured
eglCreateImageKHR:  failed to create image for buffer 0x1 target 12465 error 0x300c
eglCreateImageKHR failed.
```

不过不要担心；如果看到此错误，则只需更改一个配置设置即可使其工作。

该错误表示GPU（图形处理单元）没有足够的内存来运行演示。当将3D图形绘制到屏幕上时，正是GPU承担了所有繁重的工作，有点像游戏PC中的图形卡。树莓派在CPU和GPU之间共享其内存（RAM），并且默认情况下配置为仅给GPU提供64 MB的RAM。如果将其增加到128 MB，应该可以解决该问题。

为此，您需要输入以下命令：

```bash
sudo raspi-config
```

这将在蓝色背景上打开一个菜单。执行以下操作：

- 转到高级选项（Advanced Options）。
- 转到内存分割（Memory Split）。
- 删除`64`，然后输入`128`。按`输入`。
- 选`down`来完成。
- 点击Yes并重启（reboot）.

重新登录后，输入以下命令以返回`hello_teapot`演示：

```bash
cd /opt/vc/src/hello_pi/hello_teapot
```

现在尝试再次运行它，您应该会发现它可以工作。

```bash
./hello_teapot.bin
```

该演示将永远运行直到您退出。 要退出演示，请按Ctrl +C。
