---
layout: post
title: "使用github pages搭建个人博客"
date:   2015-09-07 15:17:20
categories: 日常
---
## 0x00 序
之前一直在第三方博客站点写点东西，由于各种限制，后来转移到阿里云上的ACE创建了wordpress，用着也挺好，可是最近ACE开始收费了，而我的那点东西不值得去花那个钱去买服务，后来发现github提供博客服务，使用的是静态页面，于是开始捣腾了一翻，顺便记录下。

## 0x01 创建github pages站点
* 首先你得拥有一个github账号，如果不会可自行到网上查阅。。。
* 创建github库，地址: [https://github.com/new](https://github.com/new)，这个仓库的名字需要和你的账号对应， 如 chinasun021.github.io，输入Description信息（可选），其他默认,然后点击创建仓库。这时即创建成功一个名为chinasun021.github.io的空库，这里先不急着创建文件，后续我们直接将模板导入到该库中即可。

## 0x02 jekyll环境搭建
由于个人使用的是windows 7 x64位系统，所以这里介绍下jekyll在windows下的安装过程。

###安装ruby
1. 前往 [http://rubyinstaller.org/downloads/](http://rubyinstaller.org/downloads/)下载rubyinstaller
2. 选择对应的版本下载，如Ruby 2.2.3 (x64)是适于64位 Windows 机器上的 Ruby 2.1.5 x64 安装包。
3. 安装下载下来的可执行文件，使用默认安装目录，并勾选“Add Ruby executables to your PATH”
4. 打开一个命令提示行并输入以下命令来检测 Ruby 是否成功安装。
	
	`ruby -v`

输出如下：

	ruby 2.1.5p273 (2014-11-13 revision 48405) [x64-mingw32]

说明ruby已安装成功

###安装DevKit
DevKit 是一个在 Windows 上帮助简化安装及使用 Ruby C/C++ 扩展如 RDiscount 和 RedCloth 的工具箱。

1. 再次前往 [http://rubyinstaller.org/downloads/](http://rubyinstaller.org/downloads/)
2. 下载同系统及 Ruby 版本相对应的 DevKit 安装包。 例如，DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe 适用于64位 Windows 系统上的 Ruby 2.0.0 x64。
3. 运行安装包并解压缩至某文件夹，如 C:\DevKit
4. 通过初始化来创建 config.yml 文件。在命令行窗口内，输入下列命令：

<pre><code class="markdown">cd “C:\DevKit”
ruby dk.rb init</code></pre>
5. 编辑config.yml，在末尾添加新的一行：
<code>- C:\Ruby21-x64</code>
6. 执行安装：
<code>ruby dk.rb install</code>

###安装Jekyll
* 确保gem已经正确安装:

<code>gem -v</code>

输出如下：

<code>2.2.2</code>

* 安装jekyll gem

<code>gem install jekyll</code>

###安装Pygments（非必须）
Jekyll 里默认的语法高亮插件是 Pygments。 它需要安装 Python 并在网站的配置文件_config.yml 里将 highlighter 的值设置为pygments。
在windows下安装失败。

###启动Jekyll
执行下面代码，然后访问[http://localhost:4000](http://localhost:4000)，就可以访问刚刚创建好的blog了。
<pre><code class="markdown">jekyll new myblog
cd myblog
jekyll serve</code></pre>

## 0x03 使用jekyll模板
jekyll模板官方站点：[http://jekyllthemes.org/](http://jekyllthemes.org/)
我找了一个github上的模板使用：[HCG](https://github.com/Gaohaoyang/gaohaoyang.github.io)

使用方法：

1.下载模板库：

<code>git clone https://github.com/Gaohaoyang/gaohaoyang.github.io</code>

2.下载我们之前创建的空git库 

<code>git clone https://github.com/chinasun021/chinasun021.github.io</code>

3.将模板库中的文件复制到chinasun021.github.io文件夹中（不要复制隐藏文件、文件夹）

4.修改模板中的_config.yml，然后更新到github服务器上，这时就可以查看[http://chinasun021.github.io](http://chinasun021.github.io)页面了

## 0x04 添加rakefile
前面下载的模板库中没有rakefile，这样创建文件不太方便，于是从网上找了一个rakefile，并做了一些修改，可以到我的[github](https://github.com/chinasun021/chinasun021.github.io)上查看，下面说明下其使用方法：

* 创建一篇文章的方法：rake post title="title"（title为要创建的文章标题），执行后会生成"%Y-%m-%d-title.md"的文件,文件内容如下：
<pre><code class="markdown">---
layout: post
title: "test"
date:   2015-09-07 17:27:45
categories:
---</code></pre>

* 创建一个页面的方法：rake page name="about.md"(about.md为要创建的页面名)，文件内容如下：
<pre><code class="markdown">---
layout: page
title: "About"
date:   2015-09-07 17:28:17
description: ""
---</code></pre>

## 0x05 如何编写文章
我使用的编写文章的工具：sublime text 2+Markdown Preview插件。

###安装Markdown Preview插件
1.【Ctrl+Shift+P】，输入pic

2.在插件搜索框输入Markdown Preview选择该插件，回车

3.稍等片刻，让 Sublime Text 自动下载安装完成，重启sublime编辑器。

###编辑Markdown文档
1.【Ctrl+N】新建一个文档

2.使用Markdown语法编辑文档：【Ctrl+Shift+P】，输入ssm选择Set Syntax:MarkDown后回车

###在浏览器中预览Markdown文档

1.【Ctrl+Shift+P】，输入mp后选择Markdown Preview:Preview in Browser

2.在浏览器预览Markdown文档

## 0x06 参考资料
http://blog.csdn.net/kong5090041/article/details/38408211