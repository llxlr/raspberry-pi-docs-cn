# OMXPlayer: 一个加速的命令行媒体播放器

安装在Raspbian的是一个命令行媒体播放器，叫作 OMXPlayer。 这是一个硬件加速并可以播放许多流行的音频和视频文件格式的播放器。

OMXPlayer由Kodi项目的Edgar Hucek开发。

OMXPlayer 使用由Raspberry Pi官方支持的OpenMAX (omx) 硬件加速接口 (媒体API) 。

## 基本用法

最简单的命令行 `omxplayer <媒体文件名>`。媒体文件可以是音频或视频，或两者都可以。对于以下示例，我们使用了Raspbian标准安装随附的H264视频文件。

```
omxplayer /opt/vc/src/hello_pi/hello_video/test.h264
```

默认情况下，音频被发送到模拟端口。如果您正在使用带扬声器并配备HDMI的显示设备，则需要通过HDMI线告诉omxplayer发送音频信号。

```
omxplayer --adev hdmi /opt/vc/src/hello_pi/hello_video/test.h264
```

显示视频时，整个显示将用作输出。您可以使用窗口选项指定要在视频的显示部分。 

```
omxplayer --win 0,0,640,480 /opt/vc/src/hello_pi/hello_video/test.h264

```
You can also specify which part of the video you want to be displayed: this is called a crop window. This portion of the video will be scaled up to match the display, unless you also use the window option.

```
omxplayer --crop 100,100,300,300 /opt/vc/src/hello_pi/hello_video/test.h264
```
If you are using the Raspberry Pi Foundation's touchscreen display, and you want to use it for video output, use the display option to specify which display to use. `n` is 5 for HDMI, 4 for the touchscreen.

```
omxplayer --display n /opt/vc/src/hello_pi/hello_video/test.h264
```
## 播放期间可用的选项

There are a number of options available during playback, actioned by pressing the appropriate key. Not all options will be available on all files. The list of key bindings can be displayed using `omxplayer --keys`:

```
    1           decrease speed
    2           increase speed
    <           rewind
    >           fast forward
    z           show info
    j           previous audio stream
    k           next audio stream
    i           previous chapter
    o           next chapter
    n           previous subtitle stream
    m           next subtitle stream
    s           toggle subtitles
    w           show subtitles
    x           hide subtitles
    d           decrease subtitle delay (- 250 ms)
    f           increase subtitle delay (+ 250 ms)
    q           exit omxplayer
    p / space   pause/resume
    -           decrease volume
    + / =       increase volume
    left arrow  seek -30 seconds
    right arrow seek +30 seconds
    down arrow  seek -600 seconds
    up arrow    seek +600 seconds

```

## 所有命令行选项

这是自2016年9月23日起构建的可用选项的完整列表，使用 `omxplayer --help` 展示:

```
 -h  --help                  Print this help
 -v  --version               Print version info
 -k  --keys                  Print key bindings
 -n  --aidx  index           Audio stream index    : e.g. 1
 -o  --adev  device          Audio out device      : e.g. hdmi/local/both/alsa[:device]
 -i  --info                  Dump stream format and exit
 -I  --with-info             dump stream format before playback
 -s  --stats                 Pts and buffer stats
 -p  --passthrough           Audio passthrough
 -d  --deinterlace           Force deinterlacing
     --nodeinterlace         Force no deinterlacing
     --nativedeinterlace     let display handle interlace
     --anaglyph type         convert 3d to anaglyph
     --advanced[=0]          Enable/disable advanced deinterlace for HD videos (default enabled)
 -w  --hw                    Hw audio decoding
 -3  --3d mode               Switch tv into 3d mode (e.g. SBS/TB)
 -M  --allow-mvc             Allow decoding of both views of MVC stereo stream
 -y  --hdmiclocksync         Display refresh rate to match video (default)
 -z  --nohdmiclocksync       Do not adjust display refresh rate to match video
 -t  --sid index             Show subtitle with index
 -r  --refresh               Adjust framerate/resolution to video
 -g  --genlog                Generate log file
 -l  --pos n                 Start position (hh:mm:ss)
 -b  --blank[=0xAARRGGBB]    Set the video background color to black (or optional ARGB value)
     --loop                  Loop file. Ignored if file not seekable
     --no-boost-on-downmix   Don't boost volume when downmixing
     --vol n                 set initial volume in millibels (default 0)
     --amp n                 set initial amplification in millibels (default 0)
     --no-osd                Do not display status information on screen
     --no-keys               Disable keyboard input (prevents hangs for certain TTYs)
     --subtitles path        External subtitles in UTF-8 srt format
     --font path             Default: /usr/share/fonts/truetype/freefont/FreeSans.ttf
     --italic-font path      Default: /usr/share/fonts/truetype/freefont/FreeSansOblique.ttf
     --font-size size        Font size in 1/1000 screen height (default: 55)
     --align left/center     Subtitle alignment (default: left)
     --no-ghost-box          No semitransparent boxes behind subtitles
     --lines n               Number of lines in the subtitle buffer (default: 3)
     --win 'x1 y1 x2 y2'     Set position of video window
 --win x1,y1,x2,y2       Set position of video window
 --crop 'x1 y1 x2 y2'    Set crop area for input video
 --crop x1,y1,x2,y2      Set crop area for input video
 --aspect-mode type      Letterbox, fill, stretch. Default is stretch if win is specified, letterbox otherwise
 --audio_fifo  n         Size of audio output fifo in seconds
 --video_fifo  n         Size of video output fifo in MB
 --audio_queue n         Size of audio input queue in MB
 --video_queue n         Size of video input queue in MB
 --threshold   n         Amount of buffered data required to finish buffering [s]
 --timeout     n         Timeout for stalled file/network operations (default 10s)
 --orientation n         Set orientation of video (0, 90, 180 or 270)
 --fps n                 Set fps of video where timestamps are not present
 --live                  Set for live tv or vod type stream
 --layout                Set output speaker layout (e.g. 5.1)
 --dbus_name name        default: org.mpris.MediaPlayer2.omxplayer
 --key-config <file>     Uses key bindings in <file> instead of the default
 --alpha                 Set video transparency (0..255)
 --layer n               Set video render layer number (higher numbers are on top)
 --display n             Set display to output to
 --cookie 'cookie'       Send specified cookie as part of HTTP requests
 --user-agent 'ua'       Send specified User-Agent as part of HTTP requests
 --lavfdopts 'opts'      Options passed to libavformat, e.g. 'probesize:250000,...'
 --avdict 'opts'         Options passed to demuxer, e.g., 'rtsp_transport:tcp,...'

```
