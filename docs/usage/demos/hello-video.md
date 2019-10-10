# Hello video

这将播放15秒长的全高清1080p视频剪辑，没有声音。这里的目的是演示视频解码和播放功能。您会看到视频非常流畅（但愿）！

![Big Buck Bunny screenshot](https://github.com/White-Album-Lab/raspberry-pi-docs-cn/blob/master/docs/usage/demos/images/bbb.jpg)
 
输入以下命令以定位到`hello_video`文件夹并列出文件：

```bash
cd ..
cd hello_video
ls
```

您会再次注意到`.bin`文件。不过，我们需要在运行此演示时告诉该演示播放哪个视频片段，所以该演示必须是`test.h264`文件（h264是一种视频编解码器）。

您将需要`./`来再次指定当前目录：

```bash
./hello_video.bin test.h264
```

现在，您应该可以看到视频剪辑的播放。它取材自开源电影[Big Buck Bunny](https://en.wikipedia.org/wiki/Big_Buck_Bunny)。
