---
title: git流程
date: 2018-5-24 09:56:10
categories:
- git
tags:
- git
---

### 步骤

#### 1. 新建分支

  `git checkout -b 类型/任务编号_任务内容`

  > -b 代表 branch，即新建一个分支

  > 类型有以下几种：
  > * feature：功能分支
  > * hotfix：补丁分支
  > * release：预发分支

#### 2. 撰写提交信息，提交分支commit

  ```
  git add --all
  git commit -m "type(scope): subject

    body

    footer
  "
  ```

  > git add . 提交modified和new（git 2.0和git add --all等效）
  >
  > git add -u 即 update，提交modified和deleted
  >
  > git add --all 或者 -A，提交modified、new和deleted

  > type有以下几种：
  > * build：影响构建系统或外部依赖的改变
  > * chore：构建过程或辅助工具的变动
  > * ci：改变ci配置文件和脚本
  > * docs：即documentation，文档
  > * feat：即feature，新功能
  > * fix：修复bug
  > * perf：代码更改，提高性能
  > * refactor：重构（既不是新增功能，也不是修复bug）
  > * release: 发布新版本
  > * style：格式（不影响代码运行的变动）
  > * test：增加测试
  > * wip：移除文件或代码
  >
  > scope代表本次commit影响的范围，比如app/test、shared/share-foot、webpack
  >
  > subject以动词开头，第一人称现在时，不用句号
  >
  > body是对subject的补充，可省略
  >
  > footer放置不兼容变更和issue关闭的信息，可省略
  >
  > 特殊情况是revert，用于撤销以前的commit，比如 revert: feat(pencil): add 'graphiteWidth' option


#### 3. 与主干同步，合并commit

  ```
  git fetch origin
  git rebase -i oigin/master
  ```

  > git fetch是获取更新，git pull是应用更新（origin代表的仓库的版本）
  > 
  > git merge 会合并两个分支为一个新的分支
  > 
  > git rebase 会取消掉一条分支并将它的改动应用到另一条分支，看上去好像只有一条分支
  > -i即--interactive，可以从多个commit中选择需要的保留

#### 4. 推送到远程仓库

  `git push --force origin 我的分支名`

  > 因为rebase以后分支历史改变了，可能跟远程分支不兼容，所以要用--force强行推送

#### 5. 发出pull request

  在仓库pull request（即PR，在gitlab中被称为merge request）到master分支，请求别人进行代码review，确认合并到master
