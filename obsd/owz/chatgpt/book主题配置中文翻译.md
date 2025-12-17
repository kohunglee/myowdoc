

```toml
# （可选）如果使用Google Analytics来跟踪您的网站，请在此设置
# 请务必将此项置于配置文件顶部，否则将无法正常工作
googleAnalytics = "UA-XXXXXXXXX-X"

# （可选）如果提供Disqus短名称，将在所有页面上启用评论功能
disqusShortname = "my-site"

# （可选）如果在文件名中使用大写字母，请将此设置为true
disablePathToLower = true

# （可选）将此设置为true可在"doc"类型页面上启用"最后修改者"日期和git作者信息
enableGitInfo = true

# （可选）该主题专为文档使用而设计，因此不渲染分类法
# 您可以使用以下配置删除相关文件
disableKinds = ['taxonomy', 'taxonomyTerm']

[params]
  # （可选，默认为light）设置颜色主题：light、dark或auto
  # 主题'auto'根据浏览器/操作系统偏好设置，在深色和浅色模式之间切换
  BookTheme = 'light'

  # （可选，默认为true）控制页面右侧目录的可见性
  # 起始和结束级别可通过markup.tableOfContents设置进行控制
  # 您也可以在页面的前置参数中单独指定此参数
  BookToC = true

  # （可选，默认为none）设置书籍徽标的路径。如果徽标位于
  # /static/logo.png，则路径应为'logo.png'
  BookLogo = 'logo.png'

  # （可选，默认为'favicon.png'）设置网站的favicon路径
  # 如果favicon位于/static/custom.svg，则路径应为'custom.svg'
  BookFavicon = 'favicon.png'

  # （可选，默认为docs）指定要渲染为菜单的内容部分
  # 您也可以将其设置为"*"以将所有部分渲染为菜单
  BookSection = 'docs'

  # （可选，默认为none）设置页面提交链接的模板。需要启用enableGitInfo
  # 启用后，将在页面页脚显示"最后修改"和指向提交的链接
  # 该参数作为模板执行，使用.Site、.Page和.GitInfo作为上下文
  BookLastChangeLink = 'https://github.com/alex-shpak/hugo-book/commit/{{ .GitInfo.Hash }}'

  # （可选，默认为none）设置编辑页面链接的模板
  # 启用后，将在页面页脚显示"编辑此页面"链接
  # 该参数作为模板执行，使用.Site、.Page和.Path作为上下文
  BookEditLink = 'https://github.com/alex-shpak/hugo-book/edit/main/exampleSite/{{ .Path }}'

  # （可选，默认为'January 2, 2006'）配置页面上使用的日期格式
  # - 在git信息中
  # - 在博客文章中
  # https://gohugo.io/functions/time/format/
  BookDateFormat = 'January 2, 2006'

  # （可选，默认为true）使用flexsearch启用搜索功能
  # 索引是动态构建的，因此可能会减慢您的网站速度
  # 索引配置可在每个语言的i18n文件夹中调整
  BookSearch = true

  # （可选，默认为true）在页面上启用评论模板
  # 默认情况下，partials/docs/comments.html包含Disqus模板
  # 参见 https://gohugo.io/content-management/comments/#configure-disqus
  # 可通过页面前置参数中的相同参数进行覆盖
  BookComments = true

  # /!\ 这是一个实验性功能，可能在任何时候被移除或更改
  # （可选，实验性，默认为false）在markdown页面中启用可移植链接和链接检查
  # 可移植链接旨在与文本编辑器配合使用，让您无需使用{{< relref >}}短代码即可编写markdown
  # 如果markdown中引用的页面不存在，主题将打印警告
  BookPortableLinks = true

  # /!\ 这是一个实验性功能，可能在任何时候被移除或更改
  # （可选，实验性，默认为false）启用服务工作者，用于缓存访问过的页面和资源以供离线使用
  BookServiceWorker = true

```

和

```toml
# 如果您希望在配置的部分之外渲染页面，或者渲染除'docs'之外的其他部分，请将类型设置为'docs'
type = 'docs'

# 设置页面权重以重新排列文件树菜单中的项目
weight = 10

# （可选）设置为'true'可将页面标记为文件树菜单中的扁平部分
bookFlatSection = false

# （可选）设置为隐藏该级别的嵌套部分或页面。仅适用于文件树菜单模式
bookCollapseSection = true

# （可选）设置为true以从侧边菜单中隐藏页面或部分
bookHidden = false

# （可选）设置为'false'可从页面隐藏目录
bookToC = true

# （可选）如果您已为站点启用BookComments，可以为特定页面禁用它
bookComments = true

# （可选）设置为'true'可将页面从搜索索引中排除
bookSearchExclude = false

# （可选）为菜单中此页面设置显式href属性
bookHref = ''

# /!\ 这是一个实验性功能，可能在任何时候被移除或更改
# （可选）为页面的菜单实体设置图标，图标将从`assets/icons`文件夹中发现
bookIcon = 'calendar'
```
