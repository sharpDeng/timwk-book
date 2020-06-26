
# 新建github项目

1. 登录 [github](https://github.com) 账号;
2. 按一下操作进行新建：
    * 点击页面右上角 `+` 号 --> `new repository`；
    * 填好项目名称（Repository name) 和 项目描述（Description）；
    * `Initialize this repository with a README` 选项可选可不选，这个选中则会在新建的仓库中自动生成一个`README.md` 文件
    * `Add .gitignore` 选择 `node`, 这会生成一个`git`的忽略文件
    * `add a license` 选择 `MIT license`即可, 这是一个开源证书
    * 最后点击 `Create repository` 即可生成一个远程仓库
3. 将远程仓库用 `git clone <path>` 拉取到本地
4. 进入到项目根目录，使用命令行`git branch gh-pages` 新建一个`gh-pages`的 git 分支(后续部署需要用到)

# 构建gitbook

1. 下载相关依赖 `npm i -g gitbook-cli`
2. 进入到上述第三步拉取下来带本地的`github`项目的根目录, 新建`README.md`（简介）、`SUMMARY.md`（目录）;
3. 然后新建章节文件 `chapter01.md`, `chapter02.md`;
4. 新建配置文件`book.json`
5. 给文件添加内容：

编写简介文件，就是

```markdown
// README.md
# 这里项目简介文件
...
```

编写目录文件

```markdown
// SUMMARY.md
# 目录

* [简介](README.md)
* [第一章](chapter01.md)
* [第二章](chapter02.md)
...
```

编写章节文件

```markdown
// chatper01.md
# 这是第一章节内容
。。。

// chatper02.md
# 这是第二章节内容
...
```

配置文件内容

```javascript
// book.json
{
    "root": "",  // 根目录，需要填你的github的repository name
    "title": "自动化构建说明", // 项目的名称
    "author": "timwk"   // 作者
}

// 注：该文件是 json 文件，应严格按照json文件格式编写
```

这样就得到一个gitbook项目了，然后接下我们要把项目代码github上，同时部署到github上；

# 项目部署

## 生成成产包

1. 先在`.gitignore`文件最后添加`_book/` 语句(这个是`gitbook`项目生成的生产包文件)
1. 先将更改的代码使用`git add -all` 和 `git commit -m "提交信息"`提交到本地仓库；
1. 使用`gitbook build` 生成生产包`_book`（这个文件部署到web服务器上即可访问了）

## 部署到github上

1. 终端进入到`_book`文件夹中，新建`git`仓库，然后使用`git remote add origin <path>`和远程仓库进行关联
2. 将代码提交到本地仓库，然后使用`git push -u origin master:gh-pages`将内容推送到远程仓库的`gh-pages`分支上(如远程仓库没有该分支会新建分支)
3. 浏览器打开 `https://<accountName>.github.io/<repository name>/` 即可打开已部署的项目，例如： [https://sharpDeng.github.io/timwk-book/](https://sharpDeng.github.io/timwk-book/)

上面是人工发布部署的步骤，下面我们来看看自动部署;
