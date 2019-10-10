# Hello Audio

该演示仅演示音频输出。它播放正弦波，发出一种`WOO WOO WOO`声音。

```bash
cd ..
cd hello_audio
ls
```

注意到绿色的`.bin`文件了吗？运行它。 你现在明白了吗？

```bash
./hello_audio.bin
```

这将通过树莓派上的耳机插孔播放声音。如果您使用的是HDMI监视器，则可以通过在命令中添加1来使其通过HDMI输出：

```bash
./hello_audio.bin 1
```

该演示将永远运行直到您退出。要退出演示，请按Ctrl +C。
