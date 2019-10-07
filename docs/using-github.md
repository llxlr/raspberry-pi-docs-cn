# 为树莓派做贡献

所有Raspberry Pi文档的资源都在线存储在一个名为GitHub的站点上，位于这里：

https://github.com/raspberrypi/documentation

虽然你不能在官方仓库直接更改文档，但是你可以查看所有源文件，并查看所有内容的排列方式。源文件和文件夹遵循Raspberry Pi网站上的分层文档。

在做任何改变前，明智的做法是找出您的贡献是否可能被接受通过检查[这里](https://www.raspberrypi.org/documentation/CONTRIBUTING.md)。

为了提交新的或更正的文档，你必须创建一个Github账号（如果您还没有一个） 然后 **fork** 原始仓库到你的账户。您可以根据自己的需要进行更改，在你的仓库保存它们，然后做一个叫做 **pull request** 的请求到原始的 Raspberry Pi 仓库。之后这个可以被维护者评估的拉取请求 (**PR**) 出现在Raspberry Pi仓库，复制编辑，然后，如果适用，会与官方存储库合并。

Raspberry Pi网站上显示的文档是从GitHub存储库生成的，并且大约每小时更新一次。

您将需要一个GitHub帐户来执行以下任何操作。

## Fork这个库

很简单。 转到Raspberry Pi仓库，https://github.com/raspberrypi/documentation，并查看页面的右上角。应该有一个标有 **Fork** 的按钮，它将存储库的副本存储到您自己的GitHub帐户中。

## 做出更改

在你自己的仓库副本中，你现在可以更改或添加文件。 文件格式是Markdown，也就是说新文件应该是 `.md` 后缀。[这里](https://guides.github.com/features/mastering-markdown/) 有GitHub的Markdown说明。

编辑文件，首先在文件名树里找到文件， 然后点击它。This displays the page in fully rendered markup, and on the toolbar at the top of the document (not top of the page) is a small icon of a pencil. This is the edit button. Click on it and the file will appear in the Github editor. You can now edit away to your heart's content. You can click on **Preview changes** to see the fully rendered file with your edits.  

在页面末尾是一个叫 **Commit Changes** 的框。 You can either commit your changes directly to your own master branch or create a new branch for use as a pull request. Use the master option, as this means you are making changes to your master copy. Using the branch option will create a new branch in your own repository, but that's a little more complicated to deal with so it won't be described here. If you are making a lot of independent changes over time before pushing the changes to Raspberry Pi, you may wish to investigate the branch option. Update the commit title and enter a description of the change at this point. 

选择 **Commit changes** 将对您的主分支进行更改。现在，您需要进行更改并从中发出请求。

## 打开一次PR

这很容易。点击在工具栏里的 **Pull Requests** 标签。之后，应该在工具栏下面有一个标记着 **New pull request** 的绿色按钮。 点击它，然后会出现一个页面，要求您比较更改。此PR页面实际上位于Raspberry Pi的GitHub页面上，而不是贡献者的，因为PR请求Raspberry Pi存储库维护者从贡献者的存储库中“拉取”。左侧应该是 `raspberrypi/documentation` 仓库，分支应该是master。右侧是 PR 来源：你的 GitHub 账号和你的 master 分支。在页面的更下方，您应该看到要在PR中拥有的提交列表，以及其下的实际更改。

如果您很高兴创建PR，点击 **Create pull request**。

就酱紫。现在，Raspberry Pi文档的PR列表中将包含您的条目。它将被读取，评估技术正确性，传递给副本编辑器以进行最终检查，最后合并到主文档树中。

这是通过GitHub进行贡献的非常快速的指南，但是它可以帮助您入门并让您有所作为！
