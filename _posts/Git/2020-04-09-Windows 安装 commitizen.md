---
layout: post
title:  "Windows 安装 commitizen"
categories: [Git]
tag: [版本控制，commit message]
---

* content
{:toc}


> **关于 nvm，nodejs，npm 的区别**
> 
> * nvm：nodejs 版本管理工具
> * nodejs：是项目开发时所需要的代码库
> * npm：nodejs 包管理工具，能够让 JS 程序员分享和复用代码的工具，JS 程序员可以通过 npm 高效地管理和发布自己要分享的代码。安装 nodejs 时，npm 也会跟着安装。
> 
> 总结一下就是：nvm 管理 nodejs 和 npm 的版本，npm 管理 nodejs 的第三方插件。

	  
## 安装 nvm

> 安装前，如果环境变量中已经有 NVM_HOME，NVM_SYMLINK，以及 PATH 中已经含有关于 nvm-noinstall 的环境变量则需要删除后再进行操作。


* 在 [nvm github](https://github.com/coreybutler/nvm-windows/releases) 处下载 nvm-noinstall.zip 压缩包。
* 将 noinstall.zip 解压到要安装的位置。
* 用记事本 install.cmd 文件，修改 NVM_SYMLINK 的值为 "%NVM_PATH%\node.js"
* 以管理员身份运行 install.cmd，输入路径：D:\application\nvm-noinstall
> 如果生成的 setting.txt 文件中的 root 和 path 是空，则重新执行一次。然后将第一次的 setting.txt 文件删除(一般在 C 盘根目录下)。
> 
> 如果失败，则删除 setting.txt 文件，删除环境变量中的 NVM_HOME，NVM_SYMLINK，以及 PATH 中已经含有关于 nvm-noinstall 的变量，再重新操作一下

## 安装 nodejs

> 可以在上一步生成的 setting.txt 文件中添加如下镜像配置(为了使下载速度更快)，这里我没有添加

	node_mirror: http://npm.taobao.org/mirrors/node/ 
	npm_mirror: https://npm.taobao.org/mirrors/npm/


安装最新版本 nodejs

	// 也可以把 latest 替换为指定版本来安装执行版本
	nvm install latest
	// 查看已安装的 nodejs 版本
	nvm list
	// 使用指定版本
	nvm use 13.12.0
	
	// nvm 其他命令
	nvm list available		// 查看网络可以安装的版本
	nvm use <ver> [arch]	// 切换使用指定版本和位数
	nvm uninstall <ver>		// 卸载指定版本
	nvm version				// 查看当前 nvm 版本

安装 nodejs，就可以使用 npm 来安装其他模块了，npm 一些基本指令如下：

	// 命令行中加入 -g 表示全局安装，全局安装直接可以在命令行使用，本地安装需要通过 require() 来引入本地安装的包
	npm install npm -g		// 旧版本的 npm 升级，
	npm install <module>	// npm 安装模块
	npm list -g				// 查看所有全局安装的模块, 可以添加 --depth 0 来看安装的模块
	npm list <module>		// 查看某个模块的版本号
	npm uninstall <module>	// 卸载模块
	npm update <module>		// 更新模块
	npm search <module>		// 搜索模块

## 安装 commitizen 
	
参考 [commitizen 全局安装](https://github.com/commitizen/cz-cli#conventional-commit-messages-as-a-global-utility)。

命令行运行：
	
	npm install -g commitizen
	
	
	// npm install -g cz-conventional-changelog	// 安装这个后，运行 `npm list -g --depth 0` 会出现 `npm ERR! missing: cz-conventional-changelog@3.0.1, required by commitizen@4.0.4` 这个提示

	// 为了可以生成 CHANGELOG.md
	npm install -g conventional-changelog
	npm install -g conventional-changelog-cli

> 我在公司的电脑上只安装了第一个命令，然后在 git 仓库中就可以使用 `git cz` 命令了。
git cz 是 git 的一个插件，git 本身并不提供，但其提供了非常强的格式管理以及良好的操作模式，使其可以完全替代 git commit。
Windows 使用此工具需要使用 windows 的 cmd 或者 powershell，以下命令执行亦是如此。

## 使用 commitizen

参考 [Commit message 和 Change log 编写指南](http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)

采用 [Angular 规范](https://docs.google.com/document/d/1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y/edit#heading=h.greljkmo14y0)，每个提交 message 包含三部分：Header，Body 和 Footer。格式如下所示：

	<type>(<scope>): <subject>
	// 空一行
	<body>
	// 空一行
	<footer>

其中，Header 是必需的，Body 和 Footer 可以省略。

不管是哪一个部分，任何一行都不得超过72个字符（或100个字符）。这是为了避免自动换行影响美观。

### Header

Header 部分只有一行，包括三个字段：type（必需）、scope（可选）和subject（必需）。

#### type

type 用于说明 commit 的类别，只允许使用下面7个标识。

	feat：新功能（feature）
	fix：修补bug
	docs：文档（documentation）
	style： 格式（不影响代码运行的变动）
	refactor：重构（即不是新增功能，也不是修改bug的代码变动）
	test：增加测试
	chore：构建过程或辅助工具的变动

如果type为feat和fix，则该 commit 将肯定出现在 Change log 之中。其他情况（docs、chore、style、refactor、test）由你决定，要不要放入 Change log，建议是不要。

> 我现在使用时，已经出现了新的其他标识

#### scope

scope用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

#### subject

subject是 commit 目的的简短描述，不超过50个字符。原则是：

	以动词开头，使用第一人称现在时，比如change，而不是changed或changes
	第一个字母小写
	结尾不加句号（.）

### Body

Body 部分是对本次 commit 的详细描述，可以分成多行。有两个注意点：

	使用第一人称现在时，比如使用change而不是changed或changes。
	应该说明代码变动的动机，以及与以前行为的对比。

### Footer
Footer 部分只用于两种情况。

* 不兼容变动

如果当前代码与上一个版本不兼容，则 Footer 部分以 BREAKING CHANGE 开头，后面是对变动的描述、以及变动理由和迁移方法。

* 关闭 Issue

如果当前 commit 针对某个issue，那么可以在 Footer 部分关闭这个 issue 。例如：

	Closes #234
	Closes #123, #245, #992

### 关于 Revert 

使用 `git revert xxxx` 指令，则会直接跳转到消息编辑器，此刻只需要退出即可，message 格式直接就是如下格式：

	revert: feat(pencil): add 'graphiteWidth' option

	This reverts commit 667ecc1654a317a13331b17617d973392f415f02.

以revert:开头，后面跟着被撤销 Commit 的 Header。Body部分的格式是固定的，必须写成This reverts commit <hash>，其中的hash是被撤销 commit 的 SHA 标识符。

如果当前 commit 与被撤销的 commit，在同一个发布（release）里面，那么它们都不会出现在 Change log 里面。如果两者在不同的发布，那么当前 commit，会出现在 Change log 的Reverts小标题下面。

## 生成 Change log

前提是所有提交都符合 Angular 格式，且必须使用 npm 安装了 conventional-changelog 和 conventional-changelog-cli。

在项目目录下运行：

	conventional-changelog -p angular -i CHANGELOG.md -s -r 0		// 在当前目录下生成 CHANGELOG.md
	conventional-changelog -p angular -i CHANGELOG.md -s			// 不覆盖以前的 CHANGELOG.md，在头部追加上次发布后的改动
