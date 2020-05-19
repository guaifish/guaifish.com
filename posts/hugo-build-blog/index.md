# 使用 Hugo 搭建静态博客网站


<!--more-->

#### 1. 安装 Hugo

Windows 安装

```cmd
scoop install hugo
```

#### 2. 生成博客

```cmd
hugo new site guaifish.com
cd guaifish.com
git init
```

#### 3. 选择主题

我使用的是 [LoveIt](https://github.com/dillonzq/LoveIt) 主题, 最好先 Fork 到自己仓库再下载

```cmd
git submodule add https://github.com/guaifish/LoveIt themes/LoveIt
```

#### 4. 配置主题

编辑 `config.toml` 配置文件, 可以参考 `themes/LoveIt/exampleSite/config.toml` 配置文件

#### 5. 添加内容

```cmd
hugo new posts/my-first-post.md
```

编辑 `content/posts/my-first-post.md` 文件内容, 注意要将 `draft` 的值设置为 `false`, 文章才会在博客上显示

#### 6. 启动 Hugo 服务器

```cmd
hugo server -D
```

可以打开 [https://localhost:1313/](https://localhost:1313/) 预览页面

#### 7. 构建静态页面

```bash
hugo -D
```

Hugo 会自动在 `public/` 目录下生成静态页面, 可以在配置文件中设置 `publicshdir` 的值更改路径

#### 参考

* [Install Hugo](https://gohugo.io/getting-started/installing)
* [Hugo Quick Start](https://gohugo.io/getting-started/quick-start/)
* [LoveIt 主题](https://hugoloveit.com/)

