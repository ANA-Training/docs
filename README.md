# Foreword

欢迎来到ANA入社考核环节，我们一共为大家准备了四个任务，时间安排和分值分配列举如下。安排这些任务的目的不是为了难，而是为了教学。我们非常欢迎学习能力强的小白，但我们不欢迎不愿意学习新知识的任何人。其中，申请者必须在第一个任务截止日期前获得至少9分，才可能具有入社资格。但是，本着以教学为主要原则，未完成Task 1目标的申请人仍然有资格参加后续的培训和任务，但无法加入研发部。但是不用担心，每一个Task都有详细的说明文档，我们不会默认被考核者具有某些先修知识。In other words, we are following one of the security principles: **Use fail-safe default**.

- <u>Sep. 16th 20:00 - Sep. 20th 23:59</u> <b>Task 1 c-basic (10 pts): </b>在这个任务中，你将熟悉C语言基本语法。
- <u>Sep. 20th 00:00 - Sep. 24th 23:59</u> <b>Task 2 upgrade-service (20 pts): </b>在这个任务中，你将熟悉C++ Standard Library（STL）的使用，并利用STL设计一个算法解决相关问题。
- <u>Sep. 24th 00:00 - Oct. 1st 23:59</u> <b>Task 3 http (30 pts): </b>在这个任务中，你将熟悉各种C语言系统调用和http服务器的构成，这些POSIX标准下的系统调用在其他语言中仍然非常有用，因为它们是基于C的。
- <u>Sep. 25th 00:00 - Oct. 8th 23:59</u> <b>Task 4 An End-to-End Encrypted File Sharing System (40 pts): </b>在这个任务中，你将熟悉Go基本语法，并使用Go开发一些接口。除此之外，我们还会介绍一些密码学相关知识，你可以选择使用或不使用这些知识设计你的接口。

## 包容性

我们希望营造一个开放和包容的学习环境，为此，我们打算支持多元化的观点和经验，并尊重所有人。同时，作为本考核的参与者，请认识到你可以积极主动地让其他同学感到被包容和受到尊重。

## 诚信政策<span id="Integrity"></span>

我们对学术诚信有最严格的要求，如果你违反了我们的学术诚信政策，将被取消本次考核成绩，并被记录在ANA诚信档案库中，永久不得加入ANA。

你可以做的：

* 向另一位同学解释一个概念，或要求另一位同学向你解释一个概念。
* 讨论项目组件的各种算法和方法。
* 讨论测试策略和方法。
* 在线搜索通用（非项目特定）抽象的算法或实现（例如，搜索哈希表的各种实现）。
* 帮助另一位同学使用高级调试方法<b>（请注意，为其他同学提供代码解决方案甚至查看他们的代码是<u>不可接受</u>的，如下所述）</b>。

你不可以做的：

- 抄袭任何其他参与考核者的代码。
- 从 CSDN、Stack Overflow、Pastebin 和 GitHub 上的公共存储库等在线资源复制代码。
- 在考核结束后公开发布你的代码。任何公开形式都不被允许，包括但不限于公开自己的student仓库、将自己的答案上传到github公共仓库等。
- 尝试破坏autograder，包括但不限于与外部用户建立网络连接、使用长输出攻击autograder、试图泄露autograder的机密等。

# Getting started

## Setup environment

首先让我们来进行环境配置，社团提供教学机器，所有环境都已经配置好，你**可以**在教学机器上完成所有考核项目。你也**可以**自己配置环境并在自己的PC上完成所有考核项目。

如果你选择在自己的PC上配置环境并且碰到了无法解决的问题，我们的社员**有权**拒绝回答此类问题，请使用教学机器。

### ssh

我们已经为所有参与考核的人建立了账户并通过apply系统发放账号密码，使用`ssh`连接到你的账户：

```bash
$ ssh netid@58.206.101.40 -p 59999
```

根据提示输入密码，再按回车，你会看到一个终端，使用这个终端，你可以执行许多Linux命令行操作。

### Git

现在让我们来学习一下Git的使用。

为了顺利获取我们为你编写好的代码框架并提交作业，我们需要和Github进行友好交流，首先，前往[Github](https://github.com)注册一个账户。如果你打不开这个网页，多尝试几次，总有一次能成功。

要让Github认识你，知道是你在访问你的个人仓库而不是什么Alice和Bob，你需要建立一对**RSA**密钥，并且把公钥上传到Github。不要担心，我们一步一步来。

**第1步**：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件，如果已经有了，可直接跳到下一步。如果没有，使用终端命令创建SSH Key：

```bash
$ ssh-keygen -t rsa -C "youremail@example.com"
```

你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。

**第2步**：使用cat命令查看公钥：

```bash
$ cat ~/.ssh/id_rsa.pub
```

它应该类似于以下内容（长度可能不同）：

```txt
ssh-ed25519 AAAAC3NzaC1lZDI1N6jpH3Bnbebi7Xz7wMr20LxZCKi3U8UQTE5AAAAIBTc2HwlbOi8T your_email@example.com
```

在浏览器中，转到[GitHub => Settings => SSH and GPG Keys => New SSH key](https://github.com/settings/ssh/new)并添加你的公钥。

- 将标题设置为可以帮助你记住该密钥所在设备的名称（例如`XJTUANA instructional machine`）。

**第3步**：尝试使用 SSH 连接到 GitHub：

```bash
ssh -T git@github.com
```

如果一切顺利，你应该看到类似以下内容：

```txt
Hi USERNAME! You've successfully authenticated, but GitHub does not provide shell access.
```

至于Git有哪些操作，如何正确使用Git，网上有非常多的教程，这里推荐一篇和我们的文档写得一样详细的Git教程：[Git教程 - 廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/896043488029600)。

### vscode

这个世界上有非常多的编辑器，在windows上有记事本，eclipse，visual studio等，在Linux上有vim，nano，gedit等。然而使用者最多，社区生态最好的编辑器，叫作**visual studio code (vscode)**。我们推荐使用vscode进行代码编辑。

在你自己的电脑上，访问vscode[下载页面](https://code.visualstudio.com/download)并找到你对应的版本。下载好以后根据引导安装即可。

通常我们下载的vscode是英文版的，对小白不太友好，若想将语言改为中文，打开**Extensions**，搜索Chinese，安装第一个。安装好以后重启，vscode就变成中文的了。

vscode的拓展插件非常丰富，我们可以使用**Remote - SSH**来连接到教学机器，搜索ssh，安装结果中的第一个。之后我们进入左边的**远程资源管理器**，鼠标放到SSH上，点击右边的'+'，将你登录教学机器的指令粘贴进去，按下回车，接着根据提示输入密码，你就可以通过vscode访问教学机器了。

除此之外，我们还推荐安装一些拓展：C/C++和Go。

## How to ask a question

请使用Github的Issues功能，你可以在我们公开的两个仓库[docs](https://github.com/ANA-Training/docs)和[student0](https://github.com/ANA-Training/student0)上提交Issues，我们的社员会不定时去解决你的问题。但请注意，提问请遵守[诚信政策](#Integrity)。你也可以在你自己的student仓库内提出私人Issues（其他人不可见），我们同样会解答你的问题。

请不要在qq群提出技术方面的问题，qq群仅用于交流考核政策(policy)方面的问题，或者闲聊。为什么？因为我们不希望一个问题被其他人的消息掩盖掉，而且我们希望看到一个问题将问题本身描述得非常详细，如果你仅仅是询问：怎么安装vscode？诸如此类的问题，我们**有权**拒绝回答。相对地，“我的代码编译不通过，编译器提示了这个错误（后面附一张图片）”这种问题，我们很乐意为你解答。