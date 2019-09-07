# FTP

FTP（文件传输协议）可用于在Raspberry Pi和另一台计算机之间传输文件。虽然使用Raspbian的默认程序`sftp-server`，具有足够权限的用户可以传输文件或目录，但也经常需要访问受限用户的文件系统。请按照以下步骤设置FTP服务器：

## 安装Pure-FTPd

首先，在终端中使用以下命令行安装`Pure-FTPd`：

```bash
sudo apt-get install pure-ftpd
```

## 基本配置

我们需要为FTP用户创建一个名为`ftpgroup`的新用户组和一个名为`ftpuser`的新用户，并确保此“user”具有** no **登录权限和** no **主目录：

```bash
sudo groupadd ftpgroup
sudo useradd ftpuser -g ftpgroup -s /sbin/nologin -d /dev/null
```

### FTP主目录，虚拟用户和用户组

例如，为第一个用户创建一个名为`FTP`的新目录：

```bash
sudo mkdir /home/pi/FTP
```

确保`ftpuser`可以访问该目录：

```bash
sudo chown -R ftpuser:ftpgroup /home/pi/FTP
```

创建一个名为`upload`的虚拟用户，将虚拟用户映射到`ftpuser`和`ftpgroup`，设置主目录`/home/pi/FTP`，并在数据库中记录用户的密码：

```bash
sudo pure-pw useradd upload -u ftpuser -g ftpgroup -d /home/pi/FTP -m
```

输入此命令行后，将需要该虚拟用户的密码。然后，键入以下命令设置虚拟用户数据库：

```bash
sudo pure-pw mkdb
```

最后但并非最不重要的是，通过建立文件`/etc/pure-ftpd/conf/PureDB`的链接来定义一个身份验证方法，数字`60`仅用于演示，使其尽可能小：

```bash
sudo ln -s /etc/pure-ftpd/conf/PureDB /etc/pure-ftpd/auth/60puredb
```

重启程序：

```bash
sudo service pure-ftpd restart
```

使用FTP客户端（如FileZilla）进行测试。

## 更详细的配置：

Pure-FTPd的配置简单直观。管理员只需要通过制作带有选项名称的文件来定义必要的设置，例如`ChrootEveryone`，然后键入`yes`，然后存储在目录`/etc/pure-ftpd/conf`中，如果所有FTP用户都是锁定在他们的FTP主目录（`/home/pi/FTP`）。以下是一些推荐的设置：

```bash
sudo nano /etc/pure-ftpd/conf/ChrootEveryone
```

输入“yes”，然后按“Ctrl + X”，“Y”和“Enter”。

同样，

创建一个名为`NoAnonymous`的文件并输入`yes`;

创建一个名为`AnonymousCantUpload`的文件并输入`yes`;

创建一个名为`AnonymousCanCreateDirs`的文件并输入`no`;

创建一个名为`DisplayDotFiles`的文件并输入`no`;

创建一个名为`DontResolve`的文件并输入`yes`;

创建一个名为`ProhibitDotFilesRead`的文件并输入`yes`;

创建一个名为`ProhibitDotFilesWrite`的文件并输入`yes`;

创建一个名为`FSCharset`的文件并输入`UTF-8`;
...

再次重新启动`pure-ftpd`并应用上述设置。

```bash
sudo service pure-ftpd restart
```

有关Pure-FTPd和文档的更多信息，请访问官方网站[Pure-FTPd](https://www.pureftpd.org/project/pure-ftpd)。
