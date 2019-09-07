# IP 地址

连接到局域网的任何设备都会分配一个IP地址。

要使用[SSH](ssh/README.md)或[VNC](vnc/README.md)从另一台计算机连接到Raspberry Pi，您需要知道Pi的IP地址。如果连接了显示器，这很容易，并且有许多方法可以从网络上的另一台机器远程查找它。

## 使用带显示屏的Pi

如果你启动到命令行而不是桌面，则应在登录提示之前的最后几条消息中显示您的IP地址。

使用终端（启动到命令行或从桌面打开终端窗口），只需键入`hostname -I`即可显示Pi的IP地址。

## 无显示器使用Pi

无需使用以下方法之一连接到屏幕，就可以找到Pi的IP地址：

### 路由器设备列表

在Web浏览器中，导航到路由器的IP地址，例如`http：// 192.168.1.1`，通常印在路由器的标签上;这将带您进入控制面板。然后使用您的凭据登录，凭据通常也会打印在路由器上或随附的文件中发送给您。浏览到已连接设备或类似设备的列表（所有路由器都不同），您应该会看到一些您认可的设备。有些设备被检测为PC，平板电脑，手机，打印机等，所以你应该认识一些并排除它们以确定哪个是你的Raspberry Pi。还要注意连接类型;如果你的Pi用线连接，应该有更少的设备可供选择。

### 用mDNS解析`raspberrypi.local`

On Raspbian, [multicast DNS](https://en.wikipedia.org/wiki/Multicast_DNS) is supported out-of-the-box by the [Avahi](https://en.wikipedia.org/wiki/Avahi_%28software%29) service.

If your device supports mDNS, you can reach your Raspberry Pi by using its hostname and the `.local` suffix.
The default hostname on a fresh Raspbian install is `raspberrypi`, so by default any Raspberry Pi running Raspbian responds to:

```bash
ping raspberrypi.local
```

If the Raspberry Pi is reachable, `ping` will show its IP address:

```
PING raspberrypi.local (192.168.1.131): 56 data bytes
64 bytes from 192.168.1.131: icmp_seq=0 ttl=255 time=2.618 ms
```

If you change the system hostname of the Raspberry Pi (e.g., by editing `/etc/hostname`), Avahi will also change the `.local` mDNS address.

If you don't remember the hostname of the Raspberry Pi, but have a system with Avahi installed, you can browse all the hosts and services on the LAN with the [`avahi-browse`](https://linux.die.net/man/1/avahi-browse) command.

### nmap command

The `nmap` command (Network Mapper) is a free and open-source tool for network discovery, available for Linux, macOS, and Windows.

- To install on **Linux**, install the `nmap` package e.g. `apt-get install nmap`.

- To install on **macOS** or **Windows**, see the [nmap.org download page](http://nmap.org/download.html).

To use `nmap` to scan the devices on your network, you need to know the subnet you are connected to. First find your own IP address, in other words the one of the computer you're using to find your Pi's IP address:

- On **Linux**, type `hostname -I` into a terminal window
- On **macOS**, go to `System Preferences` then `Network` and select your active network connection to view the IP address
- On **Windows**, go to the Control Panel, then under `Network and Sharing Center`, click `View network connections`, select your active network connection and click `View status of this connection` to view the IP address

Now you have the IP address of your computer, you will scan the whole subnet for other devices. For example, if your IP address is `192.168.1.5`, other devices will be at addresses like `192.168.1.2`, `192.168.1.3`, `192.168.1.4`, etc. The notation of this subnet range is `192.168.1.0/24` (this covers `192.168.1.0` to `192.168.1.255`).

Now use the `nmap` command with the `-sn` flag (ping scan) on the whole subnet range. This may take a few seconds:

```bash
nmap -sn 192.168.1.0/24
```

Ping scan just pings all the IP addresses to see if they respond. For each device that responds to the ping, the output shows the hostname and IP address like so:

```
Starting Nmap 6.40 ( http://nmap.org ) at 2014-03-10 12:46 GMT
Nmap scan report for hpprinter (192.168.1.2)
Host is up (0.00044s latency).
Nmap scan report for Gordons-MBP (192.168.1.4)
Host is up (0.0010s latency).
Nmap scan report for ubuntu (192.168.1.5)
Host is up (0.0010s latency).
Nmap scan report for raspberrypi (192.168.1.8)
Host is up (0.0030s latency).
Nmap done: 256 IP addresses (4 hosts up) scanned in 2.41 seconds
```

Here you can see a device with hostname `raspberrypi` has IP address `192.168.1.8`.

### Getting the IP address of a Pi using your smartphone

The Fing app is a free network scanner for smartphones. It is available for [Android](https://play.google.com/store/apps/details?id=com.overlook.android.fing) and [iOS](https://itunes.apple.com/gb/app/fing-network-scanner/id430921107?mt=8).

Your phone and your Raspberry Pi have to be on the same network, so connect your phone to the correct wireless network.

When you open the Fing app, touch the refresh button in the upper right-hand corner of the screen. After a few seconds you will get a list with all the devices connected to your network. Scroll down to the entry with the manufacturer "Raspberry Pi". You will see the IP address in the bottom left-hand corner, and the MAC address in the bottom right-hand corner of the entry.

### 更多工具

也可以看[lsleases](https://github.com/j-keck/lsleases)
