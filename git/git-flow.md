# Git workflow

## 分支管理

`develop/` ：开发者分支

`feature/`： 新功能开发

- 分支来源：develop
- 合并到分支：develop

`bugfix/`：问题修复

`release/`： 从 `development`  分支拉取，不应该开发新功能，只有错误修复、文档生成等面向发布的任务，最终合并到 `main` 分支。在 `main` 分支的 commit 中打上 tag

- 分支来源：develop
- 合并到分支：develop、main

`hotfix/` ：紧急线上故障修复，也就是 `main` 分支，更新完后应该合并到 `develop` 和 `main` 分支或者当前的 `release` 分支

- 分支来源：main
- 合并到分支：develop、 main

`chore/`：依赖升级代码重构

## Github Flow

GitHub flow是一个轻量级的、基于分支的工作流。它只保留一条长期主分支 `main`，所有新功能、修复或实验都在独立的短生命周期分支 `feature/*` 上进行，适合小团队快速交付

## 示例

前置条件：创建一个 github 远程仓库

```shell
git checkout -b feature/hello
git add main.py 
git commit -m "feat: hello example"
git push origin feature/hello
```

提交之后 github 就会有提示，根据提示操作审核通过就可以创建 feature/hello 分支，也就是发起一个 pr (pull request)，这个新分支就会多一个 main.py 文件

然后在 pull request 页码就可以选择合并 feature/hello 到 main 分支，切回 main 分支 git pull 拉取最新代码

**在本地合并**

```shell
git checkout -b feature/hello
git add main.py
git commit -m "feat: hi v2!"
git checkout main
git merge --no-ff feature/hello
git push origin main
```

## 参考

[gitflow-workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)

[Git 分支管理策略总结](https://juejin.cn/post/6844904203115036685)

[Git Flow: A Successful Git branching model](https://gist.github.com/HeratPatel/271b5d2304de2e2cd1823b9b62bf43e0)

