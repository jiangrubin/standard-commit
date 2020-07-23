## 前言

在多人协作开发项目时，如果没有规范约束 git commit message，容易造成各种提交的风格五花八门。而规范的提交信息能让他人快速了解此次提交的目的，还可以有效的输出 CHANGELOG，对项目的管理至关重要。

## Commit message 的格式

目前应用比较广泛的是 <a href="https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#-git-commit-guidelines" target="_blank">Angular 团队的规范</a>，它的 message 格式如下：

```xml
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

`type` 用于说明 commit 的类别，可以使用如下：

- feat：新功能
- fix：修复 bug
- docs：文档修改
- style：代码格式（不影响代码运行的变动）
- refactor：代码重构（即不是新增功能，也不是修改 bug 的代码变动）
- perf：优化相关，比如提升性能、体验
- test：增加测试
- revert：回滚
- chore：其他修改，比如构建流程、依赖管理
- ...

`scope` 用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同

`subject` 是 commit 目的的简短描述

`body` 是对本次 commit 的详细描述，可以分成多行

`footer` 一些备注，通常是 BREAKING CHANGE 或修复的 bug 的链接

## Commitizen

了解规范格式后，就需要通过 <a href="https://github.com/commitizen/cz-cli" target="_blank">Commitizen</a> 借助它提供的 git cz 命令替代我们的 git commit 命令，帮助我们生成符合规范的 commit message。

推荐在本地安装的方式

```
npm install commitizen --save-dev
```

接着为 commitizen 初始化 Adapter 

在 npm 5.2+ 你可以使用 <a href="http://www.ruanyifeng.com/blog/2019/02/npx.html" target="_blank">npx</a> 来初始化 Adapter

```
npx commitizen init cz-conventional-changelog --save-dev --save-exact
```

> npm < 5.2 可以执行 `./node_modules/.bin/commitizen` 或者 `./node_modules/.bin/git-cz`

并在 package.json 中添加 npm scripts 运行脚本

package.json 会新增如下配置：

```json
"scripts": {
    "commit": "git-cz"
},
"devDependencies": {
    "commitizen": "^4.0.3",
    "cz-conventional-changelog": "^3.1.0",
},
"config": {
    "commitizen": {
      "path": "./node_modules/cz-conventional-changelog"
    }
}
```

之后就可以在项目中执行 `npm run commit` 或者 `npx git cz`，效果如下：

![](https://cdn.jsdelivr.net/gh/jrb1995/image-host/1580967235373.jpeg)

## standard-version: 自动生成 CHANGELOG

使用工具后我们的工程 commit message 应该是符合 Angular 团队那套，这样也便于我们借助 <a href="https://github.com/conventional-changelog/standard-version" target="_blank">standard-version</a> 这样的工具，自动生成 CHANGELOG。

本地安装

```shell
npm install standard-version --save-dev
```

在 package.json 添加运行脚本

```json
{
  "scripts": {
    "release": "standard-version"
  }
}
```

运行脚本后，效果大致如下：

![](https://cdn.jsdelivr.net/gh/jrb1995/image-host/1580970514212.jpeg)

更多使用特性详见其<a href="https://github.com/conventional-changelog/standard-version" target="_blank">文档</a>

## 结语

查看完整的 <a href="https://github.com/jrb1995/standard-commit" target="_blank">demo</a>

此文是适合自己的一个简单通用配置，如使用 commitlint 更严格的校验 message 以及其他自定义配置，可见以下参考资料中的链接

## 参考资料

- <a href="https://juejin.im/post/5afc5242f265da0b7f44bee4" target="_blank">优雅的提交你的 Git Commit Message</a>

- <a href="http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html" target="_blank">Commit message 和 Change log 编写指南</a>