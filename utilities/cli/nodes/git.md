# Git

- [Git](#git)
  - [[git#暫存區|暫存區]]
  - [git config](#git-config)
  - [git init](#git-init)
  - [git add](#git-add)
  - [git rm](#git-rm)
  - [git rebase](#git-rebase)
  - [git clean](#git-clean)
  - [git reset](#git-reset)
  - [git restore](#git-restore)
  - [git commit](#git-commit)
  - [git status](#git-status)
  - [git diff](#git-diff)
  - [git log](#git-log)
  - [git remote](#git-remote)
  - [git push](#git-push)
  - [git pull](#git-pull)
  - [git branch](#git-branch)
  - [git checkout](#git-checkout)
  - [git merge](#git-merge)
  - [git tag](#git-tag)
  - [git cherry-pick](#git-cherry-pick)
  - [git show](#git-show)

## 暫存區

Git 不會自動把所有已修改的檔案都放進每個 commit——那樣不好！它可能會包含你不想永久保留的變更，甚至可能把 API 金鑰之類的敏感內容隨 commit 歷史洩漏到 GitHub。

因此，檔案變更在成為 commit 的一部分之前，必須經過明確選擇。為此，Git 劃分了三個區域：工作目錄（本機檔案系統中的專案目錄，也就是實際編輯檔案的位置）、暫存區（記錄下一個 commit 將包含哪些變更的區域），以及版本庫（保存 commit 歷史與專案後設資料的地方）。

使用 [`git add`](#git-add)，你可以精確選擇每個 commit 要包含的內容。這樣既能讓 commit 保持整潔，也不必一次提交所有變更。

## git config

```sh
# 配置全局邮箱
git config --global user.email "<你的邮箱>"
# 配置全局姓名
git config --global user.name "<你的名字>"
# 重置某项配置
git config --global --unset http.proxy
# 设置仓库初始化时默认的分支名
git config --global init.defaultBranch main
# 查看配置信息
git config --list
```

## git init

```sh
cd PROJECT_ROOT
# 初始化本地仓库
git init
```

## git add

```sh
# 跟蹤新文件或将已跟蹤的文件的修改添加到暂存区
git add FILE
# 将目录的修改添加到暂存区
git add DIR
# 将当前目录所有文件、目录的修改添加到暂存区
git add .
```

## git rm

```sh
# 同时删除工作区和暂存区的文件
git rm FILE
# 递归删除
git rm -f DIR
# 从暂存区移除文件并停止跟踪
git rm --cached FILE
```

## git rebase

```sh
git rebase bugFix
# 進入交互式 rebase
git rebase -i bugFix
# 先 checkout 到 main 再 rebase
git rebase bugFix main
```

## git clean

```sh
# 删除所有未跟踪的文件
git clean -f
# 删除所有未跟踪的目录
git clean -d
# 删除未跟踪文件和目录
git clean -fd
# 预览将要删除的文件
git clean --dry-run
```

## git reset

reset 可能会造成悬空的 commit，但这些 commit 其实并没有被立即删除，Git 还会保留它们一段时间，你可以通过 git reflog 找回来

```sh
# 回退分支到上一个 commit，不重置暂存区和工作目录
git reset --soft HEAD~1
# 回退分支到上一个 commit，不重置工作目录
git reset --mixed HEAD~1
# 彻底回退到某个版本
git reset --hard COMMIT
```

## git revert

```sh
# 新增一個 commit，這個 commit 剛好抵消上次的修改
git revert main HEAD^
```

## git restore

```sh
# 放弃工作区的修改
git restore FILE
# 撤销对文件的暂存
git restore --staged FILE
# 从某个 commit 恢复单个文件内容
git restore --source=HEAD~2 <file>
```

## git commit

```sh
# 提交暂存区所有文件到版本库
git commit -m COMMENT
# 修改最後一次提交
git commit --amend
# 補交文件
git add forgotten-file.js
git commit --amend --no-edit
# 修改最近一次的提交信息
git commit --amend -m "新的提交信息"
```

## git status

```sh
# 查看本地仓库状态
git status
# 简要版
git status -s
```

## git diff

```sh
# 查看差异
# 查看工作区与暂存区之间的差异
git diff
# 查看暂存区与最新提交之间的差异
git diff --staged
# 查看两个提交之间的差异
git diff COMMIT1 COMMIT2
# 查看特定文件在两个提交之间的差异
git diff COMMIT1 COMMIT2 -- FILE
# 查看工作目录和特定提交之间的差异
git diff COMMIT

# 输出格式
# 只显示文件名
git diff --name-only COMMIT1 COMMIT2
# 补丁格式差异
git diff --patch COMMIT1 COMMIT2
```

## git log

```sh
# 查看日志
git log
# 查看日志，以及改动
git log --stat
# 查看日志，以图形方式
git log --graph
# 查看日志，以一条线的方式
git log --online
```

## git remote

```sh
# 查看遠端仓库
git remote
# 查看遠端仓库的详细信息
git remote -v
# 查看特定遠端仓库
git remote show origin
# 添加關聯遠端仓库
git remote add origin REMOTE_REPO_URL
# 取消關聯遠程
git remote rm origin
# 修改关联远程仓库
git remote set-url origin REMOTE_REPO_URL
```

## git push

```sh
# 设置上游并推送到远程仓库
git push -u orgin LOCAL_BRANCH
# 推送到远程仓库
git push REMOTE_HOST LOCAL_BRANCH:REMOTE_BRANCH
# 如果本地分支与远端分支名相同
git push REMOTE_HOST LOCAL_BRANCH
# 强制 push
git push --force REMOTE_HOST LOCAL_BRANCH
# 只有当远程分支没有被别人更新时才允许 force
git push --force-with-lease
# 将标签推送到远程仓库
git push REMOTE_HOST TAG_NAME
# 刪除遠端的 foo
git push origin :foo
```

## git pull

```sh
# 从远程仓库获取最新版本合并到本地分支
git pull REMOTE_BRANCH LOCAL_BRANCH
# git pull origin foo 相當於 git fetch origin foo + git merge origin/foo
# git pull origin foo:bar 相當於 git fetch origin foo:bar + git merge origin/bar
# 从远程仓库获取最新版本合并到本地分支，不 merge 而是 rebase
git pull --rebase
```

## git branch

```sh
# 查看所有本地分支
git branch
# 查看當前所在分支
git branch --show-current
# 查看所有本地分支以及当前提交 SHA 与 commit message
git branch -v
# 查看所有本地分支以及当前提交 SHA 与 commit message 与上游分支
git branch -vv
# 查看所有远程分支
git branch -r
# 查看所有分支
git branch -a
# 新建一个本地分支
git branch BRANCH_NAME
# 删除本地分支
git branch -d BRANCH_NAME
# 强制删除本地分支
git branch -D BRANCH_NAME
# 删除远程分支
git branch -d -r BRANCH_NAME
# 重命名本地分支
git branch -m OLD NEW
# 强制重命名本地分支
git branch -M OLD NEW
# 强制讓 feature branch 指向 main 指向的 commit
git branch -f feature main
# 为本地分支设置上游远程分支
git branch --set-upstream-to=REMOTE_NAME/REMOTE_BRANCH LOCAL_BRANCH
# 取消本地分支对上游分支的追踪
git branch --unset-upstream BRANCH_NAME
```

## git fetch

```sh
# 添加本地的 bar
git getch origin :bar
```

## git checkout

```sh
# 检出到分支
git checkout BRANCH_NAME
# 检出到标签
git checkout TAG_NAME
# 检出到節點
git checkout HASH
# 创建并切换到分支
git checkout -b BRANCH_NAME
# 创建基于标签的分支
git checkout -b BRANCH_NAME TAG_NAME
# 创建基于一個 commit 的分支
git checkout -b BRANCH_NAME HASH
# 创建一个没有历史的新分支
git checkout --orphan new-main
```

## git switch

```sh
# 检出到分支
git switch BRANCH_NAME
# 檢出到節點
git switch --detach HASH
# 基于一個 commit 创建一个新分支
git switch -c new-branch HASH
```

## git merge

```sh
# 将指定分支合并到当前分支
git merge BRANCH_NAME
```

## git tag

```sh
# 列出已有的标签
git tag
# 创建一个标签
git tag TAG_NAME
# 為一個 commit 創建標簽
git tag v1.0 HASH
# 创建带注释的标签
git tag -a TAG_NAME -m "标签说明信息"
# 创建带签名的标签
git tag -s TAG_NAME -m "标签说明信息"
# 查看标签详情
git show TAG_NAME
# 删除一个标签
git tag -d TAG_NAME
```

## git cherry-pick

...

## git show

```sh
# 查看某次特定 commit
git show HASH
```

## git describe

```sh
# 查看某個 commit 和最近的引用的關係
git describe HASH
```

## Clean unreachable commit

```sh
# 檢查不可見的 commit
git fsck --unreachable
# 清理
git gc
git prune
```

## git show-ref

可用於查看各種引用

## git submodule

```sh
# 添加子模块
git submodule add https://example.com/common.git libs/common
git commit -m "添加 common 子模块"
# 克隆包含子模块的项目
git clone --recurse-submodules PROJECT_ADDRESS
