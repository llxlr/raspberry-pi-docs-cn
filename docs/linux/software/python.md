# 安装Python包

## APT

可以在Raspbian档案中找到一些Python软件包，并可以使用APT安装。 例如：

```bash
sudo apt-get update
sudo apt-get install python3-picamera
```

这是安装软件的首选方法，因为这意味着可以使用常用的`sudo apt-get update`和`sudo apt-get upgrade`命令轻松地使安装的模块保持最新。

与Python 2.x兼容的Raspbian中的Python软件包将始终带有`python-`前缀。 因此，Python 2.x的`picamera`软件包被命名为`python-picamera`（如上例所示）。Python 3软件包始终带有`python3-`前缀。因此，要为Python 3安装`picamera`，您将使用：

```bash
sudo apt-get install python3-picamera
```

可以通过以下步骤卸载通过APT安装的软件包：

```bash
sudo apt-get remove python3-picamera
```

可以使用`purge`彻底删除它们：

```bash
sudo apt-get purge python3-picamera
```

## pip

Raspbian归档文件中并非所有Python软件包都可用，有时这些软件包可能已过期。如果在Raspbian档案中找不到合适的版本，则可以从[Python软件包索引](http://pypi.python.org/)（PyPI）安装软件包。为此，请使用`pip`工具。

pip默认安装在Raspbian Jessie中（而不是Raspbian Wheezy或Jessie Lite）。您可以使用apt安装它：

```bash
sudo apt-get install python3-pip
```

要获取Python 2版本：

```bash
sudo apt-get install python-pip
```

pip3安装Python 3的模块，pip安装Python 2的模块。

例如，以下命令为Python 3安装Unicorn HAT库：

```bash
pip3 install unicornhat
```

以下命令为Python 2安装Unicorn HAT库：

```bash
pip install unicornhat
```

**注意**: 在Raspbian Wheezy中，用于管理Python 3软件包的命令是`pip-3.2`，而不是`pip3`。

通过`pip3 uninstall`或`pip uninstall`卸载Python模块。

使用[PyPI指南](https://wiki.python.org/moin/CheeseShopTutorial#Submitting_Packages_to_the_Package_Index)将自己的Python模块上传到`pip`。
