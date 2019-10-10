# Demo程序

以下是一些示例程序，以演示树莓派的功能。

![Mandelbrot fractal](https://github.com/White-Album-Lab/raspberry-pi-docs-cn/blob/master/docs/usage/demos/images/mandelbrot.jpg)

为了运行这些程序，您需要在命令行中。树莓派可能会启动到命令行（要求您输入`startx`才能进入桌面）；如果是这样，请继续前进。否则，请使用“开始”按钮注销桌面。

```bash
pi@raspberrypi ~ $
```

这是命令提示符（上面）。 它看起来很难使用，但请不要害怕！CLI或命令行界面实际上是使用计算机的非常快速有效的方法。

首先，定位到所有演示文件所在的`hello_pi`文件夹。输入以下命令以执行此操作。提示：您可以在输入命令时使用TAB键自动完成。

```bash
cd /opt/vc/src/hello_pi
```

现在，命令提示符应类似于以下文本。蓝色部分显示您在树莓派的文件系统中的位置。

```bash
pi@raspberrypi /opt/vc/src/hello_pi $
```

如果输入`ls`并按`Enter`键，则会看到文件夹列表；每个演示都有一个。但是，在运行它们之前，必须先对其进行编译。如果您不了解这是什么或为什么需要这样做，请不要担心。只需立即按照说明进行操作，稍后我们将详细了解。

在`hello_pi`文件夹中提供了一个名为`rebuild.sh`的shell脚本，它将为您进行编译。输入以下命令以运行它；暂时忽略这货！

```bash
./rebuild.sh
```

现在，许多文本将在屏幕上滚动，但是对于本练习，您可以忽略它。它只是通过演示代码工作的编译器的输出。等待命令提示符返回，然后继续。

现在，我们终于可以开始运行一些演示了！

演示程序：

- [Hello world](docs/usage/demos/hello-world.md)
- [Hello video](docs/usage/demos/hello-video.md)
- [Hello triangle](docs/usage/demos/hello-triangle.md)
- [Hello fractal](docs/usage/demos/hello-fractal.md)
- [Hello teapot](docs/usage/demos/hello-teapot.md)
- [Hello audio](docs/usage/demos/hello-audio.md)

在`hello_pi`文件夹中尝试更多演示！
