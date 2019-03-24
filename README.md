# yuan.github.io


参考：  
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;[Jekyll中文网](https://www.jekyll.com.cn/)  
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;[Liquid语法](https://help.shopify.com/en/themes/liquid)  
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;[Git官网](https://git-scm.com/)  


# 简介
## Github是什么？
GitHub是一个利用Git进行版本控制、专门用于存放软件代码与内容的共享虚拟主机服务。
## GitHub Pages是什么？
Github Pages设计的初衷是为托管在GitHub上的项目提供介绍页面,开发者们可以通过GitHub Pages为他们的每一个项目创建一个用于介绍该项目的静态网站,不过由于他的空间免费而且稳定,因此用它搭建一个个人博客网站是再好不过了.
## Git是什么？
Git是一个开源的分布式版本控制系统,可以有效、高速的处理从很小到非常大的项目版本管理.它的作用和Svn类似,就是一个版本控制的工具,用它可以将我们写的代码提交到Github上.
## Jekyll是什么？
jekyll是一个简单的免费的Blog生成工具,将纯文本转化为静态网站和博客;由于咱们的GitHub Pages生成的是静态页面,每次更新博客都需要手动更改HTML,这就使得每次写博客都变得很麻烦,而用了这个工具以后,它会根据预先设置好的格式来生成博客内容,你就无需关心html代码,只需要把重心放在博客的写作上.
## Liquid是什么?
Liquid是一种模板语言,可以在HTML页面中使用它;而他的作用就是使用标记、对象和过滤器的组合来加载一些动态内容。

# Git 设置
- 在 github 创建仓库，并在仓库的 setting->Github Pages 中的 source 选择 master branch, 如果有自己的域名也可以自定义域名。
- 在 [jekyllthemes](http://jekyllthemes.org/) 下载自己想要使用的模板，这里我下载的是 [LessOrMore 模板](http://jekyllthemes.org/themes/Less-Or-More/)，将模板上传到自己的 GitHub 仓库中

# 安装 Jekyll
**安装curl**

    sudo apt install -y curl

**安装rvm**
参考：[http://rvm.io/rvm/security](http://rvm.io/rvm/security)

    gpg --keyserver hkp://pool.sks-keyservers.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB  #安装密钥，这是必须的,如果失败可能是网络的缘故，用手机热点试下
    
    echo 409B6B1796C275462A1703113804BB82D39DC0E3:6: | gpg2 --import-ownertrust # mpapis@gmail.com
    echo 7D2BAF1CF37B13E2069D6956105BD0E739499BDB:6: | gpg2 --import-ownertrust # piotr.kuczynski@gmail.com
    
    # 这种方法总是被墙
    curl -sSL https://get.rvm.io | sudo bash -s stable  
    # 使用下面的方法
    mkdir rvm
    cd rvm
    curl -sSL https://raw.githubusercontent.com/rvm/rvm/stable/binscripts/rvm-installer     -o rvm-installer 
    curl -sSL https://raw.githubusercontent.com/rvm/rvm/stable/binscripts/rvm-installer.asc -o rvm-installer.asc 
    gpg2 --verify rvm-installer.asc rvm-installer
    bash rvm-installer stable
    

**载入 RVM 环境**
    # 每次重新打开 shell 窗口就需要使用这条语句
    source /home/samsara/.rvm/scripts/rvm

**切换rvm源**

    $ echo "ruby_url=https://cache.ruby-china.org/pub/ruby" > ~/.rvm/user/db
    
    #$ echo "ruby_url=https://gems.ruby-china.com/pub/ruby" > ~/.rvm/user/db

**安装ruby**

    rvm requirements
    rvm install 2.6.0

**安装rubygems环境**

    gem source -l   #查看当前 rubygems 源
    gem sources --remove https://rubygems.org/
    gem sources -a https://gems.ruby-china.com/
    gem update --system

**安装jekyll**

    gem install jekyll

**安装jekyll4剑客，保证jekyll能顺畅运行，官网教程太简略了**

    gem install bundler #打包用工具
    gem install jekyll-paginate #分页设置工具
    gem install minima  #默认主题
    gem install jekyll-feed #订阅用的工具



**运行Jekyll**

    jekyll serve    #自动构建并运行jekyll服务
这时候在地址栏输入http:127.0.0.1:4000就可以查看自己辛辛苦苦搭建的博客了。

# LessOrMore
**致谢**  
+ 感谢[Less官网](http://lesscss.cn/)的样式，本Jekyll框架的样式都是基于Less官网的样式直接拷贝过来的。只是重构了JS，并且加入了Jekyll语法而已。
+ 感谢[Github](https://github.com/)提供的代码维护和发布平台
+ 感谢[Jekyll](https://jekyllrb.com/)团队做出如此优秀的产品
+ 感谢[Solar](https://github.com/mattvh/solar-theme-jekyll)的原作者[Matt Harzewski](http://www.webmaster-source.com/)，在`2014.11`-`2016.09`的两年间，我的博客选用了此样式模版

**下载**

使用git从[LessOrMore](https://github.com/luoyan35714/LessOrMore.git)主页下载项目

``` bash
git clone https://github.com/luoyan35714/LessOrMore.git
```

**配置**

`LessOrMore`项目需要配置的只有一个文件`_config.yml`，打开之后按照如下进行配置。

> 特别注意`baseurl`的配置。如果是`***.github.io`项目，不修改为空''的话，会导致JS,CSS等静态资源无法找到的错误


    bash
    name: 博客名称
    email: 邮箱地址
    author: 作者名
    url: 个人网站
    # baseurl修改为项目名，如果项目是'***.github.io'，则设置为空''
    baseurl: "/LessOrMore"
    resume_site: 个人简历网站
    github: github地址
    github_username: github用户名称
    # 请到百度统计官网[https://tongji.baidu.com/](https://tongji.baidu.com/)申请自己的网站ID并在此处替换，否则将无法正常统计访问量
    baidu_analysis: 94be4b0f9fc5d94cc0d0415ea6761ae9
    # 请到revolvermaps [http://www.revolvermaps.com/?target=setupgl](http://www.revolvermaps.com/?target=setupgl)申请自己的网站ID并在此处替换，否则将无法正常统计访问量
    revolvermaps: 5ytn1ssq6za
    

**关于统计**

本项目支持三种统计，分别是

+ [百度统计](https://tongji.baidu.com)

百度统计是后台统计，并没有再页面有任何展示，但是可以通过登录百度统计官网查看更详细的访问记录分析。
当Fork本项目之后需要去百度统计官网申请自己的baidu统计ID替换 `_config.yml` 文件中的 `baidu_analysis`。

+ [revolvermaps地图统计](http://www.revolvermaps.com/)

revolvermaps地图统计是展示在左侧当行栏的地图展示，具体展示形式可以去官网定制。
当Fork本项目之后需要去revolvermaps地图官网申请自己的统计ID， 替换`_config.yml` 文件中的 `revolvermaps`。

+ [不蒜子统计](http://busuanzi.ibruce.info/)

不蒜子统计是出现在页面右上角的`本站总访问量n次`统计，本统计会自动识别客户所对应的域名，根据不同域名统计，所以并不需要Fork本项目者做任何修改。
更多不蒜子的展示方式可以去官网查看。


**如何写文章**

在`LessOrMore/_posts`目录下新建一个文件，可以创建文件夹并在文件夹中添加文件，方便维护。在新建文件中粘贴如下信息，并修改以下的`titile`,`date`,`categories`,`tag`的相关信息，添加`* content {:toc}`为目录相关信息，在进行正文书写前需要在目录和正文之间输入至少2行空行。然后按照正常的Markdown语法书写正文。

    ``` bash
    ---
    layout: post
    #标题配置
    title:  标题
    #时间配置
    date:   2016-08-27 01:08:00 +0800
    #大类配置
    categories: document
    #小类配置
    tag: 教程
    ---
    
    * content
    {:toc}
    
    
    我是正文。我是正文。我是正文。我是正文。我是正文。我是正文。
    ```

**执行**


    ``` bash
    jekyll server
    ```

**效果**
打开浏览器并输入URL`http://localhost:4000/`,回车。



