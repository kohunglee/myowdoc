
直接访问时的 `_index.md` 是主页。

-----

# 参数

## title: 标题

## layout: 是布局

比如 landing  是空白页面

其余的都一样，有左边栏

## type: docs

可以将一个博客文章，变成 docs 格式的。

# weight: 9
优先级，数字越小，越靠前

# bookHidden: true
可以将左侧的菜单中，该项给隐藏了。

## bookToC: false
隐藏掉右侧的目录。

## bookSearchExclude: false
此页，不进行索引

## bookFlatSection: true
作用未知，好像让子目录和父级目录，左侧对齐了。


# bookCollapseSection: true
显示出了一个折叠。不确实是不是正宗的折叠。


-----

|空的部分文件|Placement放置位置|
|---|---|
|`layouts/partials/docs/inject/head.html`|在关闭 `<head>` 标签之前|
|`layouts/partials/docs/inject/body.html`|在关闭 `<body>` 标签之前|
|`layouts/partials/docs/inject/footer.html`|页面页脚内容之后|
|`layouts/partials/docs/inject/menu-before.html`|在 `<nav>` 菜单块的开头|
|`layouts/partials/docs/inject/menu-after.html`|在 `<nav>` 菜单块末尾|
|`layouts/partials/docs/inject/content-before.html`|页面内容之前|
|`layouts/partials/docs/inject/content-after.html`|页面内容之后|
|`layouts/partials/docs/inject/toc-before.html`|目录块起始处|
|`layouts/partials/docs/inject/toc-after.html`|在目录块末尾|






-----

book 主题的配置说明：

```toml
# 如果您想要在配置的章节之外渲染页面，或者渲染'docs'以外的章节，请将类型设置为'docs'
type = 'docs'

# 设置页面权重以重新排列文件树菜单中的项目。
weight = 10

# (可选) 设置为 'true' 以将页面标记为文件树菜单中的扁平章节。
bookFlatSection = false (不会用)

# (可选) 设置为隐藏该级别的嵌套章节或页面。仅适用于文件树菜单模式。
bookCollapseSection = true （不会用）

# (可选) 设置为 true 以在侧边菜单中隐藏页面或章节。
bookHidden = false

# (可选) 设置为 'false' 以隐藏页面中的目录。
bookToC = true

# (可选) 如果您已为站点启用 BookComments，可以为特定页面禁用它。
bookComments = true

# (可选) 设置为 'true' 以将页面排除在搜索索引之外。
bookSearchExclude = false

# (可选) 为此页面在菜单中设置显式的 href 属性。
bookHref = '' （不懂）

# /!\ 这是一个实验性功能，可能随时被移除或更改
# (可选) 为页面的菜单实体设置一个图标，图标从 `assets/icons` 文件夹中发现。
bookIcon = 'calendar'
```



