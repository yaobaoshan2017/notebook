# Notebook
## 第一阶段基础班c语言日常学习笔记
### Git (分布式版本控制系统)
#### 1. 什么是git? 

* Git是一款免费、开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。

* Git是一个开源的分布式版本控制系统，可以有效、高速的处理从很小到非常大的项目版本管理。Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。

* Torvalds 开始着手开发 Git 是为了作为一种过渡方案来替代 BitKeeper，后者之前一直是 Linux 内核开发人员在全球使用的主要源代码工具。开放源码社区中的有些人觉得BitKeeper 的许可证并不适合开放源码社区的工作，因此 Torvalds 决定着手研究许可证更为灵活的版本控制系统。尽管最初 Git 的开发是为了辅助 Linux 内核开发的过程，但是我们已经发现在很多其他自由软件项目中也使用了 Git。例如 很多 Freedesktop 的项目迁移到了 Git 上。
#### 2. git的特点

* 分布式相比于集中式的最大区别在于开发者可以提交到本地，每个开发者通过克隆（git clone），在本地机器上拷贝一个完整的Git仓库。 

* 下图是经典的git开发过程。

![](https://imgsa.baidu.com/baike/c0%3Dbaike92%2C5%2C5%2C92%2C30/sign=da38bc6e1a4c510fbac9ea4801304e48/a71ea8d3fd1f4134ca7667d8251f95cad0c85ed6.jpg)

#### 3. Git的功能特性： 
* 从一般开发者的角度来看，git有以下功能：
1. 从服务器上克隆完整的Git仓库（包括代码和版本信息）到单机上。
1. 在自己的机器上根据不同的开发目的，创建分支，修改代码。
1. 在单机上自己创建的分支上提交代码。
1. 在单机上合并分支。
1. 把服务器上最新版的代码fetch下来，然后跟自己的主分支合并。
1. 生成补丁（patch），把补丁发送给主开发者。
1. 看主开发者的反馈，如果主开发者发现两个一般开发者之间有冲突（他们之间可以合作解决的冲突），就会要求他们先解决冲突，然后再由其中一个人提交。如果主开发者可以自己解决，或者没有冲突，就通过。
1. 一般开发者之间解决冲突的方法，开发者之间可以使用pull 命令解决冲突，解决完冲突之后再向主开发者提交补丁。
* 从主开发者的角度（假设主开发者不用开发代码）看，git有以下功能：
1. 查看邮件或者通过其它方式查看一般开发者的提交状态。
1. 打上补丁，解决冲突（可以自己解决，也可以要求开发者之间解决以后再重新提交，如果是开源项目，还要决定哪些补丁有用，哪些不用）。
1. 向公共服务器提交结果，然后通知所有开发人员。
#### 4. git的优点
  :one: : 适合分布式开发，强调个体。 
 
  :two: : 公共服务器压力和数据量都不会太大。 
 
  :three: : 速度快、灵活。 
 
  :four: : 任意两个开发者之间可以很容易的解决冲突。 
 
  :five: : 离线工作。
#### 5. git的缺点:
  :one: : 资料少（起码中文资料很少）。 
 
  :two: : 学习周期相对而言比较长。 
 
  :three: : 不符合常规思维。 
 
  :four: : 代码保密性差，一旦开发者把整个库克隆下来就可以完全公开所有代码和版本信息。 

#### 6. Git的安装
* ubuntu linux 安装方法：
```sh
$ sudo apt-get install git
```
* Mac ox 安装方法：
```sh
$ brew install git
```
#### 7. 创建git本地仓库
```sh
$ mkdir git
$ cd git
$ mkdir c
$ cd c
$ git init
$ 
```
#### 8. 增加文件
* 复制已有的文件到当前目录里：
```sh
$ cp ../../c/*.c .
```
* 创建一个新的文件。
```sh
$ touch hello.c
$ vim hello.c   //输出hello world字符串的C语言的程序（代码）
```
#### 9. 查看目录状态
* 查看当前目录下的文件在git仓库中的状态
```sh
$ git status
```
#### 10. 跟踪文件
* 将当前目录下的所有文件， 进行跟踪。
```sh
$ git add .
```
#### 11. 配置个人用户信息
* 为提交增加个人用户信息
```sh
$ git config --global user.name "Richard"
$ git config --global user.email "leix.wang@outlook.com"  
$ git config --global core.editor vim
```
#### 12. 提交
* 向本地git仓库提交， 跟踪文件
```sh
$ git commit
```
```sh
First commit

Init commit.
```
#### 13. 查看提交信息
* 查看提交相关信息
```sh
$ git log
```
```sh
第一行： commit ID
第二行： 提交作者名子和email.
第三行： 提交的时间
第四行： 提交信息标题
第五行： 提交信息具体内容
```
### Git diff
* 查看修改源码
```sh
$ git diff
```
* 两个提交版本之间做比较
```sh
$ git diff  commitID-1 commitID-2
```
* 理解Patch标记格式的含义 

  :arrow_right: : Patch多指补丁的意思比如内存补丁、文件补丁等， 也是电脑命令程序的一种。
### 删除文件
* 删除文件后， 恢复文件
```sh
$ rm -rf hello.c
$ git status
$ git checkout hello.c
```
* 从版本库里删除文件（真正删除文件）
```sh
$ git rm hello.c (or) rm hello.c
$ git status
$ git add .
$ git commit
```
### 版本之间切换
* 根据commitID， 可以进行版本切换
```sh
$ git reset --hard commitID
```
### 忽略文件
* 忽略不需要跟踪到git仓库里的文件
```sh
$ touch .gitignore
$ vim .gitignore
-----
a.out
-----
$ git add .
$ git commit
```
### Github
1. 注册github帐号 

1. 注册邮箱，注意不要使用QQ.com 

1. 创建gitc仓库 

1. 从github将创建的gitc仓库，克隆到本地
```sh
$ git clone https://github.com/username/gitc.git
```
5. 将本地仓库与github仓库进行同步，将本地提交推送到服务器上
```sh
$ git push origin master
input username:
input password:
```
6. 更新本地仓库， 与github仓库进行同步。将服务器提交拉取到本地
```sh
$ git pull
```
### MarkDown语法
#### Markdown
* Markdown 是一种轻量级标记语言，创始人为約翰·格魯伯（John Gruber）。 它允许人们“使用易读易写的纯文本格式编写文档，然后转换成有效的XHTML(或者HTML)文档”。
* ohn Gruber 在 2004 年创造了 Markdown 语言，在语法上有很大一部分是跟 Aaron Swartz 共同合作的。这个语言的目的是希望大家使用“易于阅读、易于撰写的纯文字格式，并选择性的转换成有效的 XHTML (或是HTML)”。 其中最重要的设计是可读性，也就是说这个语言应该要能直接在字面上的被阅读，而不用被一些格式化指令标记 (像是 RTF 与 HTML)。 因此，它是现行电子邮件标记格式的惯例，虽然它也借镜了很多早期的标记语言，如：setext、Texile、reStructuredText。 许多网站都使用 Markdown 或是其变种，例如：GitHub、reddit、Diaspora、Stack Exchange、OpenStreetMap 与 SourceForge 让用户更利于讨论。
#### Github MarkDown
* Markdown 标记转成HTML的样式每个网站有自己的风格, 但整体的标记格式是统一的. 我们以github来保存相关的文档, 所以我们以github的为样式为标准.
* 以下的风格是以github的markdown的风格标准.
* 具体请参考:[github的文档](https://github.com/wangleihd/command/blob/master/markdown.md)
###  Linux基础命令 

* #### vim的基本使用
```sh
$ sudo apt-get install vim
```
1. 进入插入模式 a,i

1. 进入命令模式 Esc

1. 进入底行模式 :wq

1. 复制命令 yy

1. 粘贴 p

1. 剪切 dd

1. 移动 h,j,k,l 

1. 撤销 u

1. 替换 r
* #### 常用命令
```sh
ls　　        显示文件或目录
     -l           列出文件详细信息l(list)
     -a          列出当前目录下所有文件及目录，包括隐藏的a(all)

mkdir         创建目录
     -p           创建目录，若无父目录，则创建p(parent)

cd               切换目录
touch          创建空文件
echo            创建带有内容的文件。
cat              查看文件内容
cp                拷贝
mv               移动或重命名
rm               删除文件
     -r            递归删除，可删除子目录及文件
     -f            强制删除
```
* #### 路径操作
1. 切换目录 cd xxx
1. 列出文件名 ls
1. 获得当前绝对路径 pwd
* #### 文件操作
1. 创建文件 touch xxx
1. 拷贝文件 cp xxx yyy
1. 移动或者重命名文件 mv xxx yyy
1. 删除文件 rm xxx
* #### 目录操作
1. 创建目录 mkdir
1. 拷贝目录 cp -a
1. 移动或者重命名文件 mv xxx yyy
1. 删除文件 rm xxx -r
###   C语言编译运行以及输出

* #### 编译运行输出
1. 编译： gcc xxx.c
1. 运行： ./a.out
1. 编译生成指定名称： gcc xxx.c -o xxx
1. 运行： ./xxx
###   IF语句
* #### if 语句 
1. 一个 if 语句 由一个布尔表达式后跟一个或多个语句组成。 
```sh
if(boolean_expression)
{
   /* 如果布尔表达式为真将执行的语句 */
}

如果布尔表达式为 true，则 if 语句内的代码块将被执行。如果布尔表达式为 false，则 if 语句结束后的第一组代码（闭括号后）将被执行.

示例代码：
   int a = 10; 
   /* 使用 if 语句检查布尔条件 */
   if( a < 20 )
   {
       /* 如果条件为真，则输出下面的语句 */
       printf("a 小于 20\n" );
   }
```
2. 一个 if 语句 后可跟一个可选的 else 语句，else 语句在布尔表达式为 false 时执行. 
```sh
if(boolean_expression)
{
   /* 如果布尔表达式为真将执行的语句 */
}
else
{
   /* 如果布尔表达式为假将执行的语句 */
}
```
3. 一个 if 语句后可跟一个可选的 else if语句
```sh
if(boolean_expression)
{
   /* 如果布尔表达式为真将执行的语句 */
}
else if(condition)
{
   /* 如果布尔表达式为真将执行的语句 */
}
else
{
	/*其他情况都不满足时，执行此处代码*/		
}
```





