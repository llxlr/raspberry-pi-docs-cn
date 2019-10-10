# Python

Python是一种出色而强大的编程语言，易于使用（易于阅读和编写），借助Raspberry Pi，您可以将项目连接到现实世界。

![Python logo](https://github.com/White-Album-Lab/raspberry-pi-docs-cn/blob/master/docs/usage/python/images/python-logo.png)

Python的语法非常简洁，强调可读性，并使用标准的英语关键字。首先从桌面打开IDLE。

## IDLE

对Python最简单的介绍是通过Python开发环境IDLE。 从桌面或应用程序菜单中打开IDLE：

![Python在应用菜单](https://github.com/White-Album-Lab/raspberry-pi-docs-cn/blob/master/docs/usage/python/images/app-menu-python3.png)

IDLE为您提供了一个REPL（读取，评估，打印，循环），提示您可以输入Python命令。 因为它是REPL，所以您甚至可以在不使用`print`的情况下将命令输出打印到屏幕上。

**注意**: 提供了两个版本的Python（Python 2和Python3）。Python3于2008年首次发布，Python 2的开发以2.7（于2010年发布）结束。建议使用Python 3，但Python 2可用于具有以下功能但还不支持Python 3的旧应用。

你可以根据需要来使用变量，甚至可以像计算器一样使用它。 例如：

```python
>>> 1 + 2
3
>>> name = "Sarah"
>>> "Hello " + name
'Hello Sarah'
```

IDLE还内置有语法高亮功能，并且对自动补全功能提供了一些支持。您可以使用“ Alt + P”（上一个）和“ Alt + N”（下一个）来回看您在REPL中输入的命令的历史记录。

## Python 基本用法

用Python打印Hello World:

```python
print("Hello world")
```

就那么简单！

### 缩进

某些语言使用大括号`{`和`}`来包裹属于同一行的代码块，然后让编写者缩进这些行以使其看起来嵌套。但是，Python不使用花括号，而是需要缩进嵌套。例如Python中的`for`循环：

```python
for i in range(10):
    print("Hello")
```

缩进在这里是必需的。缩进的第二行将成为循环的一部分，而缩进的第二行将在循环之外。例如：

```python
for i in range(2):
    print("A")
    print("B")
```

将会打印：

```
A
B
A
B
```

而以下：

```python
for i in range(2):
    print("A")
print("B")
```

将会打印：

```
A
A
B
```

### 变量`Variables`

要将值保存到变量，请按以下方式分配它：

```python
name = "Bob"
age = 15
```

请注意，未使用这些变量指定数据类型，因为可以推断类型，以后可以更改。

```python
age = 15
age += 1  # 将年龄增加1
print(age)
```

这次我在增量命令旁边使用了注释。

### 注释

在程序中注释被忽略，以井号“＃”表示。多行注释使用三引号，如下所示：

```python
"""
这是一个非常简单的Python程序，打印“ Hello”。
这就是全部。
"""

print("Hello")
```

### 列表`list`

Python还具有列表（在某些语言中称为数组），这些列表是任何类型数据的集合：

```python
numbers = [1, 2, 3]
```

列表用方括号`[]`表示，每一项用逗号分隔。

### 迭代

某些数据类型是可迭代的，这意味着您可以遍历它们包含的值。例如一个列表：

```python
numbers = [1, 2, 3]

for number in numbers:
    print(number)
```

这将获取`number`列表中的每一项并打印该项：
```
1
2
3
```

注意，我用`number`一词来表示每项。这只是我选择的单词，建议你的变量名选择描述性单词（见名知意），列表名使用复数形式，并且每项的单数形式都有意义。它使阅读更易理解。

其他数据类型是可迭代的，例如字符串：

```python
dog_name = "BINGO"

for char in dog_name:
    print(char)
```

这会遍历每个字符并打印出来：

```
B
I
N
G
O
```

### Range（范围）

整数类型不可迭代，尝试对其进行迭代将产生错误。例如：

```python
for i in 3:
    print(i)
```

将会报错：

```python
TypeError: 'int' object is not iterable
```

![Python error](https://github.com/White-Album-Lab/raspberry-pi-docs-cn/blob/master/docs/usage/python/images/python-error.png)

但是，您可以使用range函数来创建可迭代的对象：

```python
for i in range(3):
    print(i)
```

`range(5)`包含数字`0`，`1`，`2`，`3`和`4`（总共5个数）。使用`range(1, 6)`获取数字`1`到`5`(包括的)。

### 长度

可以使用`len`函数来查找字符串或列表的长度：

```python
name = "Jamie"
print(len(name))  # 5

names = ["Bob", "Jane", "James", "Alice"]
print(len(names))  # 4
```

### If 语句

流程控制使用`if`语句：

```python
name = "Joe"

if len(name) > 3:
    print("Nice name,")
    print(name)
else:
    print("That's a short name,")
    print(name)
```

## IDLE中的Python文件

要在IDLE中创建Python文件，请点击“文件`File > New File`，然后会出现一个空白窗口。这是一个空文件，而不是Python提示符。在此窗口中编写一个Python文件，保存它，然后运行它，将在另一个窗口中看到输出。

例如在新窗口中键入：

```python
n = 0

for i in range(1, 101):
    n += i

print("The sum of the numbers 1 to 100 is:")
print(n)
```

然后保存文件（`File > Save` or `Ctrl + S`）并运行（`Run > Run Module` or hit `F5`），将在原窗口中看到输出。

## 在命令行执行Python文件

你可以在一个标准[编辑器](docs/linux/usage/text-editors.md) 写Python文件，像是Vim，Nano，或者LeafPad, 然后在命令行运行Python脚本。只需导向文件存储的目录（使用cd和ls命令）并使用python3运行即可，例如`python3 hello.py`

![Python命令行](https://github.com/White-Album-Lab/raspberry-pi-docs-cn/blob/master/docs/usage/python/images/run-python.png)

## 其他使用Python的方式

### 命令行

通过在终端中键入`python3`可以访问标准的内置Python shell。

此shell提示您准备输入Python命令。您可以使用与IDLE同样方式来使用它，但是它没有语法高亮或自动补全功能。您可以使用 <kbd>Up/Down</kbd> 键回顾在REPL中输入的命令的历史记录。使用`Ctrl + D`退出。

### IPython

IPython是一个交互式Python shell，具有语法高亮，自动补全，漂亮的打印，内置文档等功能。默认情况下未安装IPython。安装方式：

```bash
sudo pip3 install ipython
```

然后在命令行运行`ipython`。它的工作方式类似于标准的python3，但具有更多功能。尝试键入`len?`并回车。显示包括len函数的文档信息：

```python
Type:       builtin_function_or_method
String Form:<built-in function len>
Namespace:  Python builtin
Docstring:
len(object) -> integer

Return the number of items of a sequence or mapping.
```

尝试理解以下字典：

```python
{i: i ** 3 for i in range(12)}
```

这将完美打印以下内容：

```python
{0: 0,
 1: 1,
 2: 8,
 3: 27,
 4: 64,
 5: 125,
 6: 216,
 7: 343,
 8: 512,
 9: 729,
 10: 1000,
 11: 1331}
```

在标准的Python shell中，这将打印在一行上：

```python
{0: 0, 1: 1, 2: 8, 3: 27, 4: 64, 5: 125, 6: 216, 7: 343, 8: 512, 9: 729, 10: 1000, 11: 1331}
```

![Python vs ipython](https://github.com/White-Album-Lab/raspberry-pi-docs-cn/blob/master/docs/usage/python/images





/python-vs-ipython.png)

您可以使用 <kbd>Up/Down</kbd> 键（如在python中）来查看在REPL中输入的命令的历史记录。历史记录还会保留到下一个会话，因此您可以退出`ipython`并返回（或在v2/3之间切换），历史记录仍然存在。使用`Ctrl + D`退出。

## 安装Python库

### apt

可以在Raspbian档案中找到一些Python软件包，并可以使用apt安装，例如：

```bash
sudo apt update
sudo apt install python-picamera
```

这是一种较好的安装方法，因为这意味着可以使用常用的`sudo apt update`和`sudo apt upgrade`命令轻松地使安装的模块保持最新。

### pip

Raspbian档案中并非所有Python软件包都可用，有时这些软件包可能已过时。如果在Raspbian档案中找不到合适的版本，则可以从[Python软件包索引](http://pypi.python.org/)（称为PyPI）安装软件包。

为此，请安装pip：

```bash
sudo apt install python3-pip
```

然后使用`pip3`安装Python软件包（例如`simplejson`）：

```bash
sudo pip3 install simplejson
```

在[这](docs/linux/software/python.md)阅读有关在Python中安装软件的更多信息。

#### piwheels

官方Python软件包索引（PyPI）托管由软件包维护者上传的文件。 一些软件包需要编译（编译C / C ++或类似代码）才能安装，这可能是一项耗时的工作，尤其是在单核Raspberry Pi 1或Pi Zero上。

piwheels是一项服务，提供可在Raspberry Pi上使用的预编译软件包（称为*Python wheel*）。Raspbian Stretch已预先配置为使用piwheel进行pip。在[www.piwheels.org](https://www.piwheels.org/)上了解有关piwheels项目的更多信息。

## 更多

- [使用Python的GPIO](usage/gpio/python/README.md)
- [官方Python网站](https://www.python.org/)
- [官方Python文档](https://www.python.org/doc/)
