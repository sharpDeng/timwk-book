
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

# 构建gitbook

1. 下载相关依赖 `npm i -g gitbook-cli`
2. 进入到上述第三步拉取下来带本地的`github`项目的根目录, 新建`README.md`（简介）、`SUMMARY.md`（目录）;
3. 然后新建章节文件 `chapter01.md`, `chapter02.md`;
4. 给文件添加内容：

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

这样就得到一个gitbook项目了，然后接下我们要把项目代码github上，同时部署到github上；

# 项目部署

1.