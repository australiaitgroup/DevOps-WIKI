## Development Process (作为developer)
- Dev阶段使用本地环境，可能使用docker
- Test/Integration
- UAT(User Acceptance Testing) 需要DevOps帮助 ，BA或者QA测试是否满足Acceptance Criteria

## Terraform + Lambda + API Gateway + Nodejs架构
- DevOps可以尝试这个架构
- Cloudformation vs Terraform
- Lambda很切合Nodejs

## 开发流程
- 按照jira里的ticket，在ticket里点击”Create a branch“，切换到bitbucket，创建好branch
- 在你的本地电脑，checkout 创建好的branch，在该branch 里进行开发
- 当开发完，在你的Current Branch里，对你的代码进行git commit & push，把代码push到remote branch里
- feature完整开发完，要在Pull request前，在bitbucket/githubu里，检查代码是否有conflicts，是否有落后master的代码
- 如果有落后的代码或者代码有code conflicts，对你的branch进行git rebase，进入rebase流程
- 在bitbucket或者github里，检查完代码的diff后，没有问题的，进行create a pull request
- 注意：pull request描述需要是人类能读懂的完整段落，切记不要把commit message的history当做pull request的描述。
- 在jira里把该ticket移动到code review column
- 组员和组长，tutor和老师对代码进行Code review，approval后，进行merge
- 将ticket移动到testing，由BA QA UI等进行测试，确定满足所有Acceptance Criteria


## Rebase流程
- 第一步:切换checkout到正在开发的currnet feature branch，把没有提交的代码commit & push到remote feature branch
- 第二步:切换checkout到master，pull最新的master代码到本地master branch
- 第三步:checkout到你需要rebase的feature branch，进行git rebase。git rebase onto master。也就是对该branch基于master进行rebase。
- 第四步:在Rebase中，会出现code conflicts，去fix code conflicts；rebase中可以进行squash，减少commit数量
- 第五步:Rebase结束后，Push 你的feature branch rebase完的代码到远程feature branch
- 第六步:打开bitbucket或者github，检查一下diff，查看rebase完后的代码是不是对的，如果是有问题的，继续commit 新的change到你的branch
- [tutorial: atlassian git rebase vs merge](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)

## Jira相关
- 创建时选择Scrum
- 通过ticket可以直接创建branch
- 可以直接从master检出branch, 也可以创建一个dev branch

## ticket相关
- 有一个ticket作为一个界面的底座，这类ticket通常较小，要提前完成，否则会block后续的ticket
- 界面上每一部分作为不同ticket分别开发
- 尽量分开开发减少conflict
- 如果需要，一个ticket可以创建多个branch
- 要经常进行rebase 最好每天
- squash rebase
