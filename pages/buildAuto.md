# 自动化构建

## Travis CI

>完成了项目创建，现在我们进入我们的主题--自动化构建

### 关于 Travis CI

1. 默认执行两个脚本
    * `- npm install`  安装项目依赖
    * `- npm test`      执行测试
2. `Travis CI` 默认依次执行以下九个脚本
    * before_install
    * install  //安装项目依赖，默认值是 `npm installl`
    * before_script
    * script   // 执行构建任务，包括单元测试,默认值 `npm test`
    * after_success 或 after_failure 或 after_script  // success 是前面script执行成功后执行， failure则是失败后执行，
    * after_script: script 步骤之后执行
    * before_deploy(可选)
    * deploy(可选)  // 执行部署任务
    * after_deploy (可选)

### 步骤

1. 登录，使用你的 `github`账号登录 [Travis CI](https://travis-ci.org/);
    ***注：travis CI 是有两个域名网站的，一个是.com结尾，面向的是收费用户，一个是.org结尾，面向的是社区用户，我们用的是.org社区的，小伙伴们不要搞错***
2. 关联项目，在首页的左边栏中，有个`My Repositories` 处有个 `+`, 点击进入新添自动化项目，按照 `Repositories`选项 --> `GitHub Apps Integration` 的搜索栏中输入 `timwk-book`(你的gitbook项目)，然后将开关打开关联项目即可
3. 新增环境变量，进入新增项目的 `setting`， 在`Environment Variables` 处新增以下自定义环境变量：
    * `USER_NAME`: 你的git的`user.name` 的值
    * `USER_EMAIL`: 你的git的 `user.email`的值
    * `GH_REF`: 你的`github` 项目路径， 我这里的是 `github.com/sharpDeng/timwk-book`
    * `BRANCH`: 部署分支，这里的值是 `gh-pages`
    * `ACC_TOKEN`: 这个是`Personal access token`,提供给`Travis CI`能上传代码到github上面的权限，这个在你的github中生成，生成过程如下：   
        在你的`github`中，鼠标点击右上角头像  --> `setting` --> `Developer settings` --> `Personal access tokens` --> `Generate new token` --> 填写 `note` 标识信息 --> `Select scopes`选择`repo`即可，这个选择赋予这个`access token`什么权限, `repo` 是能够上传代码，这里只需要这个就行 --> `Generate token` 生成token即可，然后将token赋值给`ACC_TOKEN`变量，在关闭前，先保存一下这个token,因为这个`token`只在生成时可见，你关闭页面后就无法查看了;

4. 回到本地的`timwk-book`项目中，根目录下新建`.travis.yml`文件，然后填写以下内容：

    ```yml
    language: node_js
    node_js:
    - "node"

    after_script:
    - gitbook build
    - cd ./_book
    - git init
    - git config user.name "${USER_NAME}"
    - git config user.email "${USER_EMAIL}"
    - git add .
    - git commit -m "pubish gitbook"
    - git push --force --quiet "https://${ACC_TOKEN}@${GH_REF}" master:${BRANCH}

    branch:
    only:
        - master
    ```

5. 最后我们还需要进行初始化项目`npm init -y`  
    初始化完成后，在`package.json`中做以下修改

    ```json
    {
        // ...
        "scripts": {
    -       "test": "echo \"Error: no test specified\" && exit 1",
    +       "test": "echo \"no test specified\" && exit 0"
        },
    +    "devDependencies": {
    +       "gitbook-cli": "^2.3.2"
    +    }
        //...
    }
    ```

6. 将修改的代码提交上传后，即可在`Travis CI` 中查看到项目正在构建了，构建成功后，你可以打开[https://github.com/sharpDeng/timwk-book](https://github.com/sharpDeng/timwk-book) 进行查看

以上就是自动化构建的步骤，小伙伴觉得有用的给个赞！