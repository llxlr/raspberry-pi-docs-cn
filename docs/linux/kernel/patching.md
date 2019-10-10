# 修补内核

当[building](docs/linux/kernel/building.md)您的自定义内核时，您可能希望将补丁或补丁集合（`补丁集`）应用于Linux内核。

在将补丁程序应用于上游Linux内核（`主线`）然后向下传播到树莓派内核源代码之前，通常会向补丁程序集提供更新的硬件作为临时措施。但是，存在用于其他目的的补丁集，例如，启用完全可抢占的内核以供实时使用。

## 版本识别

在下载和应用修补程序时，检查您拥有的内核版本非常重要。在内核源目录中，以下命令将向您显示源所涉及的版本：

```
$ head Makefile -n 3
VERSION = 3
PATCHLEVEL = 10
SUBLEVEL = 25
```

在这种情况下，源适用于3.10.25内核。您可以使用`uname -r`命令查看系统上正在运行的版本。

## 应用补丁

修补程序的应用方式取决于可用修补程序的格式。大多数补丁都是单个文件，并通过`patch`实用程序应用。例如，让我们下载示例内核版本并将其与实时内核补丁一起打补丁：

```bash
$ wget https://www.kernel.org/pub/linux/kernel/projects/rt/3.10/older/patch-3.10.25-rt23.patch.gz
$ gunzip patch-3.10.25-rt23.patch.gz
$ cat patch-3.10.25-rt23.patch | patch -p1
```

在我们的示例中，我们只需要下载文件，解压缩文件，然后使用cat工具和Unix管道将其传递给patch工具。

一些补丁集以邮箱格式的补丁集的形式出现，排列为补丁文件的文件夹。我们可以使用Git将这些补丁应用到我们的内核，但是首先我们必须配置Git以在进行这些更改时让它知道我们是谁：

```bash
$ git config --global user.name "Your name"
$ git config --global user.email "your email in here"
```

完成此操作后，我们可以应用补丁：

```baah
git am -3 /path/to/patches/*
```

如有疑问，请与补丁发行商联系，后者应告诉您如何使用它们。一些补丁集将需要特定的提交来进行修补；请遵循补丁程序分发者提供的详细信息。
