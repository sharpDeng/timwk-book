# 自动化构建

## Travis CL

>完成了项目创建，现在我们进入我们的主题--自动化构建

### 步骤

1. 登录，使用你的 `github`账号登录 [Travis CL](https://travis-ci.com/);
2. 关联项目，在首页的左边栏中，有个`My Repositories` 处有个 `+`, 点击进入新添自动化项目，按照 `Repositories`选项 --> `GitHub Apps Integration` 的搜索栏中输入 `timwk-book`(你的gitbook项目)，然后将开关打开关联项目即可
3. 新增环境变量，进入新增项目的 `setting`， 在`Environment Variables` 处新增以下自定义环境变量： 
    * `USER_NAME`: 你的git的`user.name` 的值
    * `USER_EMAIL`: 你的git的 `user.email`的值
