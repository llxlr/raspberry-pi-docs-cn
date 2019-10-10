# systemd

为了在树莓派启动时运行命令或程序，您可以将其添加为服务。完成此操作后，您可以从linux提示符下启动/停止启用/禁用。

## 创建服务

在您的Pi上，为您的服务创建一个`.service`文件，例如：

myscript.service

```
[Unit]
Description=My service
After=network.target

[Service]
ExecStart=/usr/bin/python3 -u main.py
WorkingDirectory=/home/pi/myscript
StandardOutput=inherit
StandardError=inherit
Restart=always
User=pi

[Install]
WantedBy=multi-user.target
```
因此，在这种情况下，该服务将从工作目录`/home/pi/myscript`运行Python 3，该目录包含运行`main.py`的python程序。但是，您不仅限于Python程序：只需将ExecStart行更改为命令即可启动要从引导中运行的任何程序/脚本。

将此文件以root身份复制到`/etc/systemd/system`中，例如：

```bash
sudo cp myscript.service /etc/systemd/system/myscript.service
```

复制完成后，您可以尝试使用以下命令启动服务：

```bash
sudo systemctl start myscript.service
```

使用以下命令停止它：

```bash
sudo systemctl stop myscript.service
```

当您对启动和停止应用感到满意时，可以使用以下命令在重新启动时自动启动它：

```bash
sudo systemctl enable myscript.service
```

`systemctl`命令也可用于重新启动服务或从启动中禁用它！

要注意的一些事情：
+ 事物开始的顺序取决于它们的依赖关系--在网络可用之后，此特定脚本应在引导过程中相当晚地开始（请参阅“之后”部分）。
+ 您可以根据需要配置不同的依赖关系和顺序。

您可以从以下位置获取更多信息：

```bash
man systemctl
```

或在这里：https://fedoramagazine.org/what-is-an-init-system/
