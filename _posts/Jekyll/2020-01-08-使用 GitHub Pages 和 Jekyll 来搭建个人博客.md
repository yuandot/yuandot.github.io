---
layout: post
title:  "使用 GitHub Pages 和 Jekyll 来搭建个人博客"
categories: Jekyll
---

* content
{:toc}


参考链接： 

- <a href="https://help.github.com/en/github/working-with-github-pages" target="_blank">GitHub Pages</a>   

## 1 开始使用 GitHub Pages

用户可以为 project，user，organization 设置一个基本的 GitHub 主页网站。

GitHub Free 账户使用 GitHub Pages 的 repository 类型必须是 public；其他账户的 repository 类型可以是 private 或者 public。

### 1.1 关于 GitHub Pages

更多关于 [GitHub Pages 在 GitHub Developer documentation](https://developer.github.com/v3/repos/pages/)。

GitHub Pages 是一个静态站点托管服务，直接从 repository 获取 HTML，CSS，JaveScript 文件，也可以使用一个构建起使用这些文件构建，然后发布一个站点。更多<a href="https://github.com/collections/github-pages-examples" target="_blank">关于 GitHub Pages 的实例网站</a>。

可以使用 GitHub 系列以 `github.io` 结尾的域名或者使用用户申请的域名。

#### 1.1.1 GitHub Pages 类型

三种类型：

* **project** 
    * 与托管在 GitHub 上的一个 project 关联；
    * 存储在相关的 project 仓库中，如果没有使用自定义域名，则外部访问使用的域名是 `http(s)://<username>.github.io/<repository>` 和 `http(s)://<organization>.github.io/<repository>`；
    * 每个账户可以创建的数量不限。
* **user 和 organization** 
    * 与一个指定的 GitHub 账户关联；
    * 仓库名是 `<user>.github.io` 和 `<organization>.github.io`，如果没有使用自定义域名，则外部访问使用的域名是 `http(s)://<username>.github.io` 和 `http(s)://<organization>.github.io`；
    * 每个账户只能创建一个。

> 如果使用遗留的 `<user>.github.com` 名称仍然发布的仓库，外部访问者会被直接从 `http(s)://<username>.github.com` 重定向到 `http(s)://<username>.github.io`。如果 `<user>.github.com` 和 `<user>.github.io` 同时存在，仅仅 `<user>.github.io`仓库会被发布。

#### 1.1.2 GitHub Pages 的发布源

默认发布源：

* **project：** 默认是 `gh-pages` 分支，可选 `master` 分支或者 `master` 分支中的 `/docs` 文件夹。


* **user 和 organization：** 只能是 `master` 分支

#### 1.1.3 静态站点生成器

可以直接将静态站点文件直接 `push` 到仓库，也可以使用一个静态站点生成器使用仓库中的源文件来生成静态站点。推荐使用 GitHub Pages 内建支持的静态站点生成器 Jekyll。

默认情况下 GitHub Pages 会使用 Jekyll 来构建站点。如果不想使用 Jekyll，而是使用其他生成器，可以在发布源根目录下创建一个空文件 `.nojekyll`，然后按照生成器的说明来构建站点。

GihHub Pages 不支持服务端语言，例如 PHP，Ruby，Python。

#### 1.1.4 GitHub Pages 的使用

建议：

* 使能 HTTPS
* GitHub Pages 不应该用来传输敏感信息，例如密码等等
* 对 GitHub Pages 的使用受限于 [GitHub 服务条款](https://help.github.com/en/github/site-policy/github-terms-of-service)

限制：

* GitHub Pages 发布源的大小不能超过 1GB，更多信息参考 [用户硬盘配额](https://help.github.com/en/github/managing-large-files/what-is-my-disk-quota#file-and-repository-size-limitations)
* 站点大小不大于 1GB
* GitHub Pages 软件宽带限额是每月 100GB
* GitHub Pages 每显示最多 10 次构建

其他禁止使用条目可参考 [禁止使用](https://help.github.com/en/github/working-with-github-pages/about-github-pages#prohibited-uses)。

#### 1.1.5 GitHub Pages 的 MIME 类型

MIME 类型是服务器发往浏览器的包含关于文件性质和格式的头部。GitHub Pages 提供超过 750 种 MIME 类型，支持的 MIME 类型列表可以通过 [mime-db project](https://github.com/jshttp/mime-db) 来生成。

虽然为每个文件和仓库指定自定义的 MIME 类型，但是可以添加或者修改 GitHub Pages 使用的 MIME 类型，更多说明可以参考 [the mime-db contributing guidelines](https://github.com/jshttp/mime-db#adding-custom-media-types)。

### 1.2 创建一个 GitHub Pages 站点

可以在一个已经存在的仓库或者新的仓库中创建一个 GitHub Pages 站点。

* 如果没有仓库，需要先创建仓库
* repository->Setting 中选择发布源
* repository->Setting->GitHub Pages 中可以看到 URL

仓库 `push` 后，20 分钟内改变会发布到站点，如果一个小时候，改变还没有发布到站点，可查看 Jekyll Build Error。

### 1.3 使用主题选择器为 GitHub Pages 添加主题

可以使用主题选择器为仓库添加 Jekyll 主题。

主题选择器的使用依赖于仓库是 `public` 还是 `private`：

* 如果仓库开始 GitHub Pages，主题选择器可以为当前发布源添加主题
* 如果仓库是 `public` 并且 GitHub Pages 处于关闭状态，使用主题选择器将开启 GitHub Pages 并且配置 `master` 分支作为发布源
* 如果仓库是 `private` 并且 GitHub Pages 处于关闭状态，必须开启 GitHub Pages 后才能使用主题选择器

如果以前手动添加过 Jekyll 主题，这些主题在使用主题选择器后可能会被继续使用，为了避免冲突，使用主题选择器之前移除所有手动添加的主题文件。

使用主题选择器添加主题：repository->Settings->GitHub Pages->Theme Chooser

选择的主题将自动应用于存储库中的 markdown 文件，为了将主题应用到 HTML 文件中需要为每个文件添加 YAML fron matter 指定一个 layout。详细说明可参考 [Front Matter](https://jekyllrb.com/docs/front-matter/)。

关于 [Jekyll Theme](https://jekyllrb.com/docs/themes/)。

### 1.4 配置发布源

如果用户使用默认发布源，则站点自动发布。也可以为 `project` 站点选择发布源。

步骤：

* 首先确认要作为发布源的分支或者文件夹已经存在
* repository->Settings-GitHub Pages->Source 中选择发布源

如果选择mo `master` 分支中的 `docs` 文件夹作为发布源，可是删除了 `/docs` 文件夹，那么站点会构建错误，会得到一个丢失 `/docs` 文件夹的错误信息。

### 1.5 配置一个自定义的 404 页面

用户可以配置一个自定义的 404 页面，用于当访问不存在页面时的显示页面。

* 在发布源根目录下创建一个文件命名为 `404.html` 或者 `404.md`
* 如果命名为 `404.md`，需要在文件头部添加以下内容：

    ---
    permalink: /404.html
    ---


### 1.6 GitHub Pages 使用 HTTPS

HTTPS 可以阻止别人窥探和篡改站点中的内容，用户可以在 GitHub Pages 中为所有的 HTTP 强制重定向使用 HTTPS。

#### 1.6.1 关于 HTTPS 和 GitHub Pages

所有的 GitHub Pages 站点，包括使用自定义域名的站点都支持 HTTPS。

2016年6月15号以后创建的 GitHub Pages 站点强制使用 HTTPS 访问，之前创建的可以通过 repository->setting 来使能 HTTPS 访问。

#### 1.6.2 使能 HTTPS

* 打开相应仓库
* 打开 Setting
* GitHub Pages 选项下，选择 Enforce HTTPS

#### 1.6.3 使能 HTTPS 后遗留问题

如果使用 HTTPS 后，站点中的 HTML 文件仍然通过 HTTP 引用资源，则有可能会出现一些问题，可以将站点内所有 `http://` 替换为 `https://`。通常在以下位置进行替换：

* 如果使用 Jekyll，HTML 文件一般在 `_layouts` 文件夹下
* CSS 通常可以在 HTML 文件的 `<head>` 中发现
* JavaScript 通常可以在 `<head>` 内或者 `</body>` 标签前面发现
* Images 经常在 `<body>` 内发现 

### 1.7 GitHub Pages 中使用子模块

可以在 GitHub Pages 中使用子模块来将其他项目中的文件包含在站点代码中。

如果发布源中包含子模块，则站点构建时会自动将子模块内容拉进来。

用户仅仅可以将子模块指向 `public` 仓库，因为 GitHub Pages 服务器不能访问 `private` 仓库。

关于子模块更多信息，可参考 [git 子模块](https://git-scm.com/book/en/v2/Git-Tools-Submodules)。

### 1.8 撤销站点发布

可以撤销已发布的 GitHub Pages 站点，来使站点不再被外部访问。

对于 **project** 站点：

* 如果 `gp-pages` 分支是发布源，则删除 `gp-pages` 分支。
* repository->Settings->GitHub Pages->Source 中选择 None。
* 如果自定义了域名，为了避免域名被回收，请更新 DNS 配置。

对于 **user** 或者 **organization** 站点：

* 删除 `master` 分支或者删除整个仓库
* 如果自定义了域名，为了避免域名被回收，请更新 DNS 配置。

## 2 使用 Jekyll 建立一个 GitHub Pages 站点

### 2.1 关于 GitHub Pages 和 Jekyll

#### 2.1.1 关于 Jekyll
Jekyll 是 GitHub Pages 内置的静态站点生成器。Jekyll 基于用户选择的布局，使用 Markdown 文件和 HTML 文件来创建一个完整的静态网站。Jekyll 支持 Markdown 和 Liquid（可以在站点中加载动态内容的模板语言）。更多信息可参考 [Jekyll](https://jekyllrb.com/)。

Jekyll 在 Windows 中没有官方支持，可参考 [Jekyll on Windows](https://jekyllrb.com/docs/installation/windows/)。

推荐使用 Jekyll，也可以使用其他静态网站生成器，或者在本地或者另一个服务器自定义自己的构建进程。

#### 2.1.2 配置 Jekyll

通过 `_config.yml` 文件来配置大部分 Jekyll 设置，例如站点主题，插件等等，更多信息需要参考 Jekyll 中的 [Configuration](https://jekyllrb.com/docs/configuration/) 文档。

无法更改 GitHub Pages 中的某些配置：

    lsi: false
    safe: true
    source: [your repo's top level directory]
    incremental: false
    highlighter: rouge
    gist:
      noscript: false
    kramdown:
      math_engine: mathjax
      syntax_highlighter: rouge
      
      
默认情况下，Jekyll 不会构建下面文件和文件夹里的内容：

* `/node_modules` 或者 `/vendor` 
* 名字以 `_`，`.` 或者 `#` 开始
* 名字以 `~` 结尾
* 配置文件中通过 `exclude` 设置的文件

如果想要 Jekyll 处理这些文件，需要在配置文件中使用 `includes` 来设置。

#### 2.1.3 Front matter

可以在 Markdown 文件或者 HTML 文件开头添加一段 YAML front matter 为文章或者页面设置变量和元数据，例如标题，布局等等

可以给一篇文章或者页面添加 `site.github` 来将任何仓库引用元数据添加到站点。更多信息可参考 Jekyll 元数据文档中的 [Using `site.github`](https://jekyll.github.io/github-metadata/site.github/)。

#### 2.1.4 主题

更多信息可参考 Jekyll 文档中的 [Themes](https://jekyllrb.com/docs/themes/)。

可以添加 GitHub Pages [Supported themes](https://pages.github.com/themes/) 中的主题到站点中。

可以手动添加托管在 GitHub 中的[开源 Jekyll 主题](https://github.com/topics/jekyll-theme)。

可以透过编辑主题文件来覆盖主题的默认值，详情可查看主题文档和 [覆盖默认主题文档](https://jekyllrb.com/docs/themes/#overriding-theme-defaults)。

#### 2.1.5 插件

用户可以下载或者常见插件来扩展 Jekyll 的功能。例如，插件 [jemoji](https://github.com/jekyll/jemoji) 可以让用户在站点任何页面上使用 GitHub 风格的表情，就像在 GitHub 中使用的一样。更多信息可以参考 Jekyll 文档中的 [Plugins](https://jekyllrb.com/docs/plugins/) 文档。

GitHub Pages 对于下列插件模式是开启的，而且不能关闭：

* [jekyll-coffeescript](https://github.com/jekyll/jekyll-coffeescript)
* [jekyll-default-layout](https://github.com/benbalter/jekyll-default-layout)
* [jekyll-gist](https://github.com/jekyll/jekyll-gist)
* [jekyll-github-metadata](https://github.com/jekyll/github-metadata)
* [jekyll-optional-front-matter](https://github.com/benbalter/jekyll-optional-front-matter)
* [jekyll-paginate](https://github.com/jekyll/jekyll-paginate)
* [jekyll-readme-index](https://github.com/benbalter/jekyll-readme-index)
* [jekyll-titles-from-headings](https://github.com/benbalter/jekyll-titles-from-headings)
* [jekyll-relative-links](https://github.com/benbalter/jekyll-relative-links)

可以通过在 `_config.yml` 文件中添加插件的 gem 到 `plugins` 设置中来使能其他插件。更多信息可查看 Jekyll 文档中的 [Configuration](https://jekyllrb.com/docs/configuration/) 文档，对于支持的插件列表，可查看 GitHub Pages 站点的 [Dependency versions](https://pages.github.com/versions/)。

关于指定插件的使用说明，请查看相应插件的文档。

用户可以通过更新 GitHub Pages 的 gem 来确保使用所有插件的最新版本。

GitHub Pages 不能使用不支持的插件来构建站点。如果想要使用不支持的插件，请先在本地生成站点，然后推送站点的静态文件到仓库。

#### 2.1.6 语法高亮

语法高亮可以让用户的网站更容易阅读，代码片段可以向 GitHub 中那样高亮显示。关于语法高亮的信息可以参考 [创建和高亮显示代码块](https://help.github.com/en/github/writing-on-github/creating-and-highlighting-code-blocks)。

默认情况下，代码块会被 Jekyll 高亮显示。Jekyll 使用 [Rouge](https://github.com/rouge-ruby/rouge) 高亮显示器，与 [Pygments](https://pygments.org/) 兼容。如果在 `_config.yml` 文件中使用 Pygments，实际将使用 Rouge。Jekyll 将不能使用其他的语法高亮器，如果在 `_config.yml` 文件中指定其他语法生成器，构建时会得到警告。

如果想要使用另一个高亮器，必须禁止 Jekyll 的语法高亮，通过更新 `_config.yml` 文件：

    kramdown:
        syntax_highlighter_opts:
        disable : true
        
如果主题中没有包含用于语法高亮的 CSS，可以通过下面生成 GitHub 的语法高亮 CSS，然后添加到工程的 `style.css` 文件中。

    $ rougify style github > style.css
    
### 2.2 使用 Jekyll 创建 GitHub Pages 站点

使用 Jekyll 创建 GitHub Pages 站点之前，需要先安装 [Jekyll](https://jekyllrb.com/docs/installation/) 和 [Git](https://help.github.com/en/github/getting-started-with-github/set-up-git)。

> 说明：如果使用本地调试需要安装 Jekyll，如果不需要本地调试，可以不安装 Jekyll。

推荐使用 [Bundler](http://bundler.io/) 来安装和运行 Jekyll。Bundler 管理 Ruby gem 依赖，减少 Jekyll 构建错误，防止环境相关的错误。

安装 Bundler：

* [安装 Ruby](https://www.ruby-lang.org/en/documentation/installation/)
* [安装 Bundler](https://bundler.io/)

在本地初始化仓库，并构建站点，然后推送给远程仓库。

### 2.3 使用 Jekyll 进行本地测试

可以在本地构建 GitHub Pages 站点来预览站点的改变。

* 本地构建

        $ bundle exec jekyll serve
        > Configuration file: /Users/octocat/my-site/_config.yml
        >            Source: /Users/octocat/my-site
        >       Destination: /Users/octocat/my-site/_site
        > Incremental build: disabled. Enable with --incremental
        >      Generating...
        >                    done in 0.309 seconds.
        > Auto-regeneration: enabled for '/Users/octocat/my-site'
        > Configuration file: /Users/octocat/my-site/_config.yml
        >    Server address: http://127.0.0.1:4000/
        >  Server running... press ctrl-c to stop.

* 在浏览器中输入 `http://localhost:4000` 来预览

Jekyll 会频繁更新。如果本地的 `github-pages` gem 比 GitHub Pages 服务器上的 gem 更老，本地构建的站点可能看起来与发布在 GitHub 中的会不一样，为了避免这种情况，周期地更新本地的 `github-pages` gem：

* 开启 Git Bash
* 更新 `github-pages` gem
    * 如果安装了 Bundler，运行 `bundle update github-pages`
    * 如果没有安装 Bundler，运行 `gem update github-pages`

### 2.4 使用 Jekyll 向 GitHub Pages 中添加内容

#### 2.4.1 关于 Jekyll 站点中的内容

Jekyll 站点内容的主要类型是页面和文章。一个页面是不与指定日期相关的独立内容，例如 `About` 页面。Jekyll 站点默认有一个命名为 `about.md` 文件，可以在 `url/about` 页面呈现内容，也可以用这个页面作为模块来创建新的页面。更多信息可参考 Jekyll 文档中的 [Pages](https://jekyllrb.com/docs/pages/)。

一篇文章是一个博客文章，Jekyll 站点通常有一个 `_posts` 文件夹包含默认的文章文件。用户可以编辑这个文章中的内容，也可以用这个文章作为模板来创建新的文章，更多信息可参考 Jekyll 文档中的 [Posts](https://jekyllrb.com/docs/posts/)。

主题包含了默认的 `layouts`，`includes` 和 `stylesheets`，会自动应用在站点中的页面和文章中，但是用户可以覆盖这些默认设置。更多信息可参考 2.1.4 节内容。

#### 2.4.2 站点中添加页面

* 创建文件 `PAGE-NAME.md` 
* 添加下面的 YAML front matter 在文件开头，替换其中的 PAGE TITLE 和 URL-PATH

        layout: page
        title: "PAGE TITLE"
        permalink: /URL-PATH/

* YAML front matter 后面添加内容

#### 2.4.3 站点中添加文章

* 进入 `_posts` 文件夹，创建文件 `YYYY-MM-DD-NAME-OF-POST.md`
* 添加下列 YAML front matter 在文件开头。替换其中的 POST TITLE，YYYY-MM-DD hh:mm:ss -0000，CATEGORY-1 和 CATEGORY-2
* YAML front matter 后面添加内容

### 2.5 设置 Markdown 处理器

GitHub Pages 支持两种 Markdown 处理器：

* [kramdown](https://kramdown.gettalong.org/)
* [CommonMark](https://commonmark.org/)   
GitHub 拥有的扩展，可以在 GitHub 上显示 GitHub 风格 Markdown。更多信息可参考 [About writing and formatting on GitHub](https://help.github.com/en/github/writing-on-github/about-writing-and-formatting-on-github)

可以通过其他处理时使用 GitHub 风格 Markdown，但是只有 CommonMark 处理器总是完全符合在 GitHub 上的显示。

选择 Markdown 处理器的方法：在 `_config.yml` 文件中使用 `markdown: kramdown` 或者 `markdown: GFM`。

更多参考文档： [kramdown 文档](https://kramdown.gettalong.org/documentation.html)，[GitHub 风格 Markdown 规格书](https://github.github.com/gfm/)

### 2.6 添加主题

主题仓库中会提供一些帮助，例如：[Minima's README](https://github.com/jekyll/minima#customizing-templates)。

一些自定义特性最好用于 GitHub [已经支持的主题](https://pages.github.com/themes/)。


添加主题的方法：

* 对于[已经支持的主题](https://pages.github.com/themes/)，在 `_config.yml` 中添加 `theme: THEME-NAME`。
* 对于托管在 GitHub 上的其他主题，在 `config.yml` 文件中添加 `remote_theme: THEME-NAME`。

为主题添加自定义的 CSS：

* 创建文件 `/assets/css/style.scss`
* 在文件开头添加以下内容，在 `@import` 后面添加自定义的 CSS 或者 Sass

        ---
        ---
        
        @import "";


为主题自定义 HTML 布局：修改文件 `_layouts/default.html`。

### 2.7 关于 Jekyll 构建错误

当你推送改变到发布源时，GitHub Pages 没有尝试去构建站点：

* 推送者没有校验 email，更多信息可参考 [Verifying your email address](https://help.github.com/en/github/getting-started-with-github/verifying-your-email-address)
* 正在使用部署密钥推送。如果用户想要自动推送到仓库的发布源，用户可以设置一个机器用户。更多信息可参考 [管理部署密钥](https://developer.github.com/v3/guides/managing-deploy-keys/#machine-users)
* 正在没有配置构建发布源的 CI 服务。更多信息可参考 [定制化构建](https://docs.travis-ci.com/user/customizing-the-build/#safelisting-or-blocklisting-branches) 或者用户的 CI 服务文档

当 Jekyll 尝试构建时产生错误，用户会收到构建错误消息。注意有两种构建错误消息：

* 页面构建警告：意味着构建成功完成，但是需要改变来避免以后可能遇到问题
* 页面构建失败：意味着构建没有完成，如果 Jekyll 能够检测失败的原因，用户会看到错误消息的描述。

推荐推送改变之前在本地测试，这样可以在命令行看到构建错误，并且定位 bug。

当用户创建一个拉取请求来更新发布源时，用户可以在拉取请求的 Checks 标签中看到构建错误信息。更多信息可参考 [About status checks](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/about-status-checks)。

当用户推送改变到发布源时，如果构建错误或者警告时，用户会在主邮箱中收到邮件。也可以在仓库的 Settings 标签中看到构建错误信息（不包含构建警告）。

用户可以配置一个第三方服务，例如 [Travis CI](https://travis-ci.org/) 来显示错误消息：

* 发布源的根目录下添加文件 `Gemfile`，包含下面内容

        source `https://rubygems.org`
        gem `github-pages`
        
* 为站点仓库配置所选择的的测试服务。例如，使用 [Travis CI](https://travis-ci.org/) 时，需要在发布源根目录下添加文件 `.travis.yml`，包含下面内容

        language: ruby
        rvm:
          - 2.3
        script: "bundle exec jekyll build"
        
* 用户可能需要使用第三方测试服务来激活仓库，更多信息请参考第三方服务文档

### 2.8 排查构建错误

#### 2.8.1 一般错误

如果收到一般错误消息，请检查常见问题：

* 是否正在使用不支持的插件
* 仓库大小和站点文件大小是否超过仓库的大小限制
* 用户改变了 `_config.yml` 文件中的 `source` 设置。GitHub Pages 在构建中会覆盖该值
* 发布源中的文件命中包含不支持的 `:` 字符

#### 2.8.2 配置文件错误

`_config.yml` 包含语法错误，`_config.yml` 需要遵守的规则：

* 使用空格代替制表符
* 键值对中的 `:` 后面包含一个空格
* 只能使用 UTF-8 字符
* 引用任何特殊字符，例如 `:`
* 对于多行值，使用 `|` 来创建新行，使用 `>` 来忽略新行

可以通过将 YAML 文件中的内容粘贴到 YAML linter 中来识别错误，例如 [YAML Validator](https://codebeautify.org/yaml-validator)。

#### 2.8.3 日期是无效的

以为着站点中的页面包含无效的日期时间。

为了排除这个错误，在错误消息和调用日期相关 Liquid 过滤器的文件布局中搜索文件。确保任何情况下传递给 Liquid 过滤器的变量都包含值，从没有传递 `nil` 或者 `""`。更多信息可参考 [Liquid filters](https://help.shopify.com/en/themes/liquid/filters)。

#### 2.8.4 包含目录中不存在文件

意味着 `_includes` 目录下不存在代码中引用的文件。

为了排除这个错误，在错误信息中的文件中搜索 `inlcude` 来查看是否有引用其它文件，例如 `\{\% include example_header.html \%\}` 这样的语句。如果引用的文件没有存在，需要在 `_includes` 目录下添加相应文件。

#### 2.8.5 文件是一个符号链接

意味着代码中引用了一个符号链接文件，实际在发布源中不存在这个文件内容。

为了排除这个错误，在错误信息中的文件中搜索 `inlcude` 来查看是否有引用其它文件，例如 `\{\% include example_header.html \%}` 这样的语句。如果引用的文件是一个符号链接，需要在 `_includes` 目录下添加相应文件。

#### 2.8.6 文件不是 UTF-8 编码

意味着用户使用了非拉丁字符，但是没有通知计算机。

为了排除这个错误，可以强制文件使用 UTF-8 编码，通过在 `_config.yml` 中添加 `encoding: UTF-8`。

#### 2.8.7 无效的高亮语言

意味着用户指定了出 [Rouge](https://github.com/rouge-ruby/rouge) 和 [Pygments](http://pygments.org/) 以外的其他语法高亮器。

为了排除这个错误，更新 `_config.yml` 文件来指定语法高亮器为 [Rouge](https://github.com/rouge-ruby/rouge) 或者 [Pygments](http://pygments.org/)。

#### 2.8.8 无效的文章日期

意味着站点中在文章名或者 YAML front matter 中包含了一个无效的日期。

为了排除这个错误，要确保所有的日期格式都是 `YYYY-MM-DD HH:MM:SS` （UTC 时间），并且是实际的日期。如果要指定时区，使用 `YYYY-MM-DD HH:MM:SS +/-TTTT`，例如： 2014-04-18 11:30:00 +0800。

如果在 `_config.yml` 文件中指定日期格式，要确保是正确的。 

#### 2.8.9 无效的 Sass 或者 SCSS

意味着仓库中包含的某个 Sass 或者 SCSS 文件中包含了无效的内容。

为了排除这个错误，在错误消息中查看无效 Sass 或者 SCSS 文件的行号。为了防止以后出现同样的错误，可以为文本编辑器安装 Sass 和 SCSS 
linter。

#### 2.8.10 无效的子模块

意味着仓库中包含了不能正确初始化的子模块。

为了排除这个错误，首先决定是否需要使用子模块，有时会意外创建子模块。如果不使用子模块，使用下列命令来移除子模块：

    $ git submodule deinit PATH-TO-SUBMODULE
    $ git rm PATH-TO-SUBMODULE
    $ git commit -m "Remove submodule"
    $ rm -rf .git/modules/PATH-TO-SUBMODULE
    
如果使用子模块，请确保使用 `https://` 来引用，且子模块必须有是 `public` 仓库。

#### 2.8.11 数据文件中无效的 YAML

意味着 `_data` 目录下的文件包含无效的 YAML

为了排除这个错误，确保 `_data` 目录下的 YAML 文件遵守：

* 使用空格代替制表符
* 键值对中的 `:` 后面包含一个空格
* 只能使用 UTF-8 字符
* 引用任何特殊字符，例如 `:`
* 对于多行值，使用 `|` 来创建新行，使用 `>` 来忽略新行

可以通过将 YAML 文件中的内容粘贴到 YAML linter 中来识别错误，例如 [YAML Validator](https://codebeautify.org/yaml-validator)。

更多关于 Jekyll 数据文件的信息，可以参考 Jekyll 文档中的 [Data Files](https://jekyllrb.com/docs/datafiles/)。

#### 2.8.12 Markdown 错误

意味着仓库中包含了 Markdown 错误。

为了排除这个错误，请确保使用了支持的 Markdwon 处理器；确保错误消息的文件中使用有效的 Markdown 语法。更多信息，可参考 [Markdown 语法](https://daringfireball.net/projects/markdown/syntax)。

#### 2.8.13 失去 docs 文件夹

意味着选择了 `master` 分支中的 `docs` 文件夹作为发布源，可是 `master` 分支中并没有 `docs` 文件夹。

为了排除这个错误，如果 `docs` 意外移动了，需要重新移动回去。如果 `docs` 意外删除了，那么用户可以选择：

* 使用 Git 回退或者撤销删除，更多信息可参考 [git-revert](https://git-scm.com/docs/git-revert.html)
* 创建新的 `docs` 文件夹
* 改变发布源

#### 2.8.14 配置相对链接

意味着在 `_config.yml` 文件中有不支持的相对永久链接。

永久链接时指向特定页面的永久 URLs。绝对永久链接以站点根开始，相对永久链接以引用页面的当前文件夹开始。GitHub Pages 和 Jekyll 不再支持相对永久链接。更多信息可参考 [Permalinks](https://jekyllrb.com/docs/permalinks/)。

为了排除这个错误，移除 `_config.yml` 文件中的 `relative_permalinks`，并且将站点内的所有相对永久链接修改为绝对永久链接。

#### 2.8.15 符号链接不存在

意味着包含了一个不存在发布源中的符号链接。

为了排除这个错误，首先确定这个符号链接是否需要，如果不需要，则删除。如果需要，则确保符号链接或者文件在发布源中。如果需要引用外部资源，可是使用子模块或者第三方包管理器，例如 [Bower](https://bower.io/)。

#### 2.8.16 for 循环中的语法错误

意味着代码中的 Liquid `for` 循环声明中存在语法错误。

为了排除这个错误，确保错误消息中文件中的所有 `for` 循环都使用正确的语法，关于语法的详情可参考 [Iteration tags](https://help.shopify.com/en/themes/liquid/tags/iteration-tags#for)。

#### 2.8.17 标签没有正确关闭

意味这个代码中包含未正确关闭的逻辑标记。例如 `\{\% capture example_variable \%\}` 必须使用 `\{\% endcapture \%\}` 来关闭。

为了排除这个错误，请确保错误消息中提到的文件中的所有逻辑标记都正确关闭。更多信息可参考标记语法 [Liquid tags](https://help.shopify.com/en/themes/liquid/tags)。

#### 2.8.18 标签没有正确终止

意味着代码中包含了为没有正确终止的输出标签。例如，不应该是 `\{\{ page.title \}`，而应该是 `\{\{ page.title \}\}`。

更多语法可参考 [Liquid objects](https://help.shopify.com/en/themes/liquid/objects)。

#### 2.8.19 其他标签错误

意味着代码中存在未识别的 Liquid 标签。

为了排除这类错误，确保错误消息中提到的文件中的所有 Liquid 标签都能够与 Jekyll 的默认变量匹配，且标签中没有拼写错误。Jekyll 中的默认变量可参考 Jekyll 文档中的 [Variables](https://jekyllrb.com/docs/variables/)。

不支持的插件是未识别标签的常见来呀。如果在本地使用不支持的插件生成站点文件，并推送到 GitHub，请确保插件没有引用不在 Jekyll 默认变量中的标签。


