## Development Process (作为 developer)

- Dev 阶段使用本地环境，可能使用 docker
- Test/Integration
- UAT(User Acceptance Testing) 需要 DevOps 帮助 ，BA 或者 QA 测试是否满足 Acceptance Criteria

## Terraform + Lambda + API Gateway + Nodejs 架构

- DevOps 可以尝试这个架构
- Cloudformation vs Terraform
- Lambda 很切合 Nodejs

## 开发流程

- 按照 jira 里的 ticket，在 ticket 里点击”Create a branch“，切换到 bitbucket，创建好 branch
- 在你的本地电脑，checkout 创建好的 branch，在该 branch 里进行开发
- 当开发完，在你的 Current Branch 里，对你的代码进行 git commit & push，把代码 push 到 remote branch 里
- feature 完整开发完，要在 Pull request 前，在 bitbucket/githubu 里，检查代码是否有 conflicts，是否有落后 master 的代码
- 如果有落后的代码或者代码有 code conflicts，对你的 branch 进行 git rebase，进入 rebase 流程
- 在 bitbucket 或者 github 里，检查完代码的 diff 后，没有问题的，进行 create a pull request
- 注意：pull request 描述需要是人类能读懂的完整段落，切记不要把 commit message 的 history 当做 pull request 的描述。
- 在 jira 里把该 ticket 移动到 code review column
- 组员和组长，tutor 和老师对代码进行 Code review，approval 后，进行 merge
- 将 ticket 移动到 testing，由 BA QA UI 等进行测试，确定满足所有 Acceptance Criteria

## Rebase 流程

- 第一步:切换 checkout 到正在开发的 currnet feature branch，把没有提交的代码 commit & push 到 remote feature branch
- 第二步:切换 checkout 到 master，pull 最新的 master 代码到本地 master branch
- 第三步:checkout 到你需要 rebase 的 feature branch，进行 git rebase。git rebase onto master。也就是对该 branch 基于 master 进行 rebase。
- 第四步:在 Rebase 中，会出现 code conflicts，去 fix code conflicts；rebase 中可以进行 squash，减少 commit 数量
- 第五步:Rebase 结束后，Push 你的 feature branch rebase 完的代码到远程 feature branch
- 第六步:打开 bitbucket 或者 github，检查一下 diff，查看 rebase 完后的代码是不是对的，如果是有问题的，继续 commit 新的 change 到你的 branch
- [tutorial: atlassian git rebase vs merge](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)

## Jira 相关

- 创建时选择 Scrum
- 通过 ticket 可以直接创建 branch
- 可以直接从 master 检出 branch, 也可以创建一个 dev branch

## ticket 相关

- 有一个 ticket 作为一个界面的底座，这类 ticket 通常较小，要提前完成，否则会 block 后续的 ticket
- 界面上每一部分作为不同 ticket 分别开发
- 尽量分开开发减少 conflict
- 如果需要，一个 ticket 可以创建多个 branch
- 要经常进行 rebase 最好每天
- squash rebase
