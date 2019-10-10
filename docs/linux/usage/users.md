# Linux用户

Raspbian中的用户管理是在命令行上完成的。默认用户为`pi`，密码为`raspberry`。您可以添加用户并更改每个用户的密码。

## 更改您的密码

以`pi`用户身份登录后，强烈建议使用`passwd`命令更改默认密码以提高树莓派的安全性。

在命令行上输入`passwd`，然后按`Enter`。系统将提示您输入当前密码进行身份验证，然后要求输入新密码。完成后按`Enter`键，系统将要求您确认。请注意，输入密码时不会显示任何字符。正确确认密码后，将显示一条成功消息（`passwd：密码更新成功`），新密码将立即生效。

如果您的用户具有`sudo`权限，则可以使用`passwd`更改其他用户的密码，并在该用户名之前添加该密码。例如，`sudo passwd bob`将允许您设置用户`bob`的密码，然后设置用户的一些其他可选值，例如用户名。只需按Enter键即可跳过这些选项。

### 删除用户密码

您可以使用`sudo passwd bob -d`删除用户`bob`的密码。

## 创建一个新用户

您可以使用`adduser`命令在Raspbian安装上创建其他用户。

输入`sudo adduser bob`，系统将提示您输入新用户`bob`的密码。如果您不需要密码，请将此字段留空。

### 主文件夹

创建新用户时，他们将在`/home/`中拥有一个主文件夹。`pi`用户的主文件夹位于`/home/pi/`中。

#### skel

创建新用户后，`/etc/skel/`的内容将被复制到新用户的主文件夹中。您可以根据需要添加或修改`/etc/skel/`中的`.bashrc`文件，并且该版本将适用于新用户。

## Sudoers

Raspbian上的默认`pi`用户是一个`sudoer`。 这样可以在以`sudo`开头时以`root`身份运行命令，并以`sudo su`切换为`root`用户。

要将新用户添加到`sudoers`中，请输入`sudo visudo`（来自sudoer用户），并在带注释的标头`＃用户权限规范`下找到`root ALL=(ALL:ALL)ALL`行。 复制此行，然后从`root`切换到用户名。要允许无密码的`root`访问，请更改为`NOPASSWD:ALL`。以下示例为用户`bob`提供了无密码`sudo`访问权限：

```bash
# User privilege specification
root  ALL=(ALL:ALL)ALL
bob   ALL=NOPASSWD:ALL
```

保存并退出以应用更改。请小心，因为可能会意外删除您自己的`sudo`权利。

您可以通过输入以下命令来更改`visudo`命令使用的编辑器（默认为Nano）。

```bash
update-alternatives --set editor /usr/bin/vim.tiny
```

这将编辑器设置为Vim。

## 删除用户

您可以使用`userdel`命令在系统上删除用户。应用`-r`标志也删除其主文件夹：

```bash
sudo userdel -r bob
```
