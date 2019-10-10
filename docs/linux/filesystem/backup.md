# 备份

强烈建议您定期备份所有重要文件。备份通常不限于用户文件；它们可能包括配置文件，数据库，已安装的软件，设置，甚至是系统的整个快照。

在这里，我们将指导您完成一些有关树莓派系统的备份技术。

## 主文件夹

备份主文件夹的明智方法是使用`tar`命令创建该文件夹的快照存档，并将其副本保留在家用PC或云存储中。为此，请输入以下命令：

```bash
cd /home/
sudo tar czf pi_home.tar.gz pi
```

这将在`/home/`中创建一个名为`pi_home.tar.gz`的tar归档文件。您应该将此文件复制到USB记忆棒或将其传输到网络上的另一台计算机。

## MySQL

如果您在树莓派上运行了MySQL数据库，那么最好也对其进行备份。要备份单个数据库，请使用`mysqldump`命令：

```bash
mysqldump recipes > recipes.sql
```

此命令会将`recipes`数据库备份到文件`recipes.sql`。注意，在这种情况下，没有向`mysqldump`命令提供用户名和密码。如果您的主文件夹中的`.my.cnf`配置文件中没有MySQL凭据，请提供带有标志的用户名和密码：

```bash
mysqldump -uroot -ppass recipes > recipes.sql
```

要从转储文件恢复MySQL数据库，请将转储文件通过管道传递到mysql命令。提供凭据（如果需要）和数据库名称。请注意，数据库必须存在，因此请首先创建它：

```bash
mysql -Bse "create database recipes"
cat recipes.sql | mysql recipes
```

另外，您可以使用`pv`命令查看进度表，因为转储文件是由MySQL处理的。默认情况下未安装，因此请使用`sudo apt-get install pv`进行安装。此命令对大文件很有用：

```bash
pv recipes.sql | mysql recipes
```

## SD卡镜像

保留整个SD卡映像的副本可能是明智的，因此，如果丢失或损坏，可以恢复该卡。您可以使用与将图像写入新卡相同的方法来执行此操作，但是相反。

在Linux中：

```bash
sudo dd bs=4M if=/dev/sdb of=raspbian.img
```

这将在您的计算机上创建一个图像文件，您可以使用该图像文件写入另一个SD卡，并保持完全相同的内容和设置。要恢复或克隆到另一张卡，请反向使用`dd`：

```bash
sudo dd bs=4M if=raspbian.img of=/dev/sdb
```

这些文件可能很大，并且压缩得很好。要进行压缩，您可以将dd的输出通过管道传递到`gzip`，以获取比原始大小小得多的压缩文件：

```bash
sudo dd bs=4M if=/dev/sdb | gzip > raspbian.img.gz
```

要恢复，请将`gunzip`的输出通过管道传递到`dd`：

```bash
gunzip --stdout raspbian.img.gz | sudo dd bs=4M of=/dev/sdb
```

如果您使用的是Mac，则使用的命令几乎完全相同，但是上述示例中的`4M`应替换为小写字母`4m`。

请参阅有关[安装SD卡映像](docs/installation/installing-images/README.md)的更多信息。

## 自动化

您可以编写一个Bash脚本来自动执行所有这些过程，甚至可以使用[cron](docs/usage/cron.md)定期执行该脚本。
