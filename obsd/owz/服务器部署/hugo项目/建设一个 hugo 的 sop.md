
中文版文档 https://hugo.opendocs.io/

然后我开启一个新的，名为 blankhugo 的项目

路径 ： /Applications/EasySrv/www/blankhugo

初始化一个仓库

----


```bash
hugo new site quickstart 
cd quickstart
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke 
echo "theme = 'ananke'" >> hugo.toml
hugo server
```

初始化！

然后在 vscode 的那个 git 处，【关闭仓库】那个 ananke 仓库。

-----

新建 hugo-book 文件夹。然后复制粘贴该主题文件。

然后 (set `theme = "hugo-book"`/`theme: hugo-book` in configuration file)

调试命令是 ： 

```bash
hugo server --minify --theme hugo-book


cp -R themes/hugo-book/exampleSite/content.en/* ./content # 复制 demo 目录
```


-----

默认情况下，主题会将 `content/docs` 部分的页面以树形结构渲染为菜单。

在页面的前置元数据中设置 `title` 和 `weight` 来调整菜单中的顺序和标题，以及其他参数以隐藏或更改菜单中的网址。您可以通过 `BookSection` 配置参数选择用于生成菜单的文件夹。


```toml
# Google Analytics跟踪网站，在此设置。
# 务必放在配置文件顶部
# googleAnalytics = "UA-XXXXXXXXX-X"

# (可选) Disqus 的 shortname，在所有页面上启用评论功能。
# disqusShortname = "my-site"

# 在‘doc’类型页面上启用‘最后修改于’日期和Git作者信息。
enableGitInfo = true

# (可选) 本主题专为文档使用设计，因此默认不渲染分类页面。
# 您可以使用下面的配置移除相关文件。
disableKinds = ['taxonomy', 'taxonomyTerm']

[params]
  # light（亮色）, dark（暗色）或 auto（自动）
  BookTheme = 'auto'

  # 页面右侧目录的可见性。
  BookToC = true

  # /static/logo.png，那么路径应为 'logo.png'。
  BookLogo = 'logo.png'

  # 如果图标在 /static/custom.svg，那么路径应为 'custom.svg'。
  BookFavicon = 'favicon.png'

  # 您也可以将值设置为 "*" 以将所有部分渲染到菜单中。
  BookSection = 'docs'

  # 页面使用的日期格式。
  BookDateFormat = 'January 2, 2006'

  # 启用使用flexsearch的搜索功能。
  # 索引是即时构建的，因此可能会减慢您的网站速度。
  # 索引配置可在每个语言的 i18n 文件夹中进行调整。
  BookSearch = true

  # (可选，默认为 true) 在页面上启用评论模板。
  # 默认情况下，partials/docs/comments.html 包含 Disqus 模板。
  # 参考：https://gohugo.io/content-management/comments/#configure-disqus
  # 可以通过页面前置参数中的相同参数覆盖此设置。
  # BookComments = true

  # /!\ 这是一个实验性功能，可能会随时被移除或更改。
  # (可选，实验性，默认为 false) 启用服务工作者（Service Worker），用于缓存已访问的页面和资源以供离线使用。
  BookServiceWorker = true
```

-----

托管到 cloudflare 上。

配置里 `baseURL = 'https://openworld.zone/' ` 改好。

然后提交到 github 里。

进入 cloudflare ，右上角添加 页面。选择我的仓库。

- 框架预设，选择 hugo，
- 构建命令 `hugo --minify` ，
- 路径，写入 quickstart ， 

然后单击 部署！

-----

多语言

将 demo 里的 文件夹，复制粘贴到 quickstart 根目录，切记，不是 content 这个目录。

然后在 配置 里写：

```toml
  

# 允许使用 html

[markup.goldmark.renderer]

unsafe = true

[languages]

	[languages.en]

	languageName = 'English'
	
	contentDir = 'content.en'
	
	weight = 1
	
	  
	
	[languages.zh]
	
	languageName = 'Chinese'
	
	contentDir = 'content.zh'
	
	weight = 2
	
	  
	
	[languages.he]
	
	languageName = 'Hebrew'
	
	contentDir = 'content.he'
	
	languageDirection = 'rtl'
	
	weight = 3
```

现在，基本上就初步可以了！