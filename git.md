### 起步
#### 安装 Git
##### 在 Windows 上安装
    打开 http://git-scm.com/download/win，下载会自动开始。 要注意这是一个名为 Git for Windows的项目（也叫做 msysGit），和 Git 是分别独立的项目。
##### 从源代码安装

#### 配置
##### 用户信息
```js
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```
##### 检查配置信息
```js 
$ git config --list 
$ git config <key> //来检查 Git 的某一项配置
```
##### 获取帮助
```js
$ git help <verb> // Git命令手册
$ git <verb> --help
$ man git-<verb>
$ git help config // config命令手册
```
### 基础
#### 获取 Git 仓库
有两种取得 Git 项目仓库的方法。 第一种是在现有项目或目录下导入所有文件到 Git 中； 第二种是从一个服务器克隆一个现有的 Git 仓库。
##### 在现有目录中初始化仓库
```js
$ git init
```
##### 克隆现有的仓库
```js
$ git clone [url]
$ git clone https:\/\/github.com/libgit2/libgit2 mylibgit //自定义本地仓库的名字。克隆libgit2仓库，并将本地仓库命名为mylibgit
```
#### 检查当前文件状态
```js
$ git status
```
#### 跟踪新文件
```js
$ git add <filename>
//  git add, 这是个多功能命令：可以用它开始跟踪新文件，或者把已跟踪的文件放到暂存区，还能用于合并时把有冲突的文件标记为已解决状态等。 
```
#### 忽略文件
 在这种情况下，我们可以创建一个名为 .gitignore 的文件，列出要忽略的文件模式。文件 .gitignore 的格式规范如下：
* 所有空行或者以 ＃ 开头的行都会被 Git 忽略。
* 可以使用标准的 glob 模式匹配。(shell 所使用的简化了的正则表达式)
* 匹配模式可以以（/）开头防止递归。
* 匹配模式可以以（/）结尾指定目录。
* 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。
#### 查看已暂存和未暂存的修改
```js
$ git diff //查看尚未暂存的文件更新了哪些部分
$ git diff --cached // 查看已暂存的文件更新了哪些部分（Git 1.6.1以上版本也可以用命令git diff --staged）
```
#### 提交更新
```js
$ git commit
$ git commit -m "Story 182: Fix benchmarks for speed" //在 commit 命令后添加 -m 选项，将提交信息与命令放在同一行
$ git commit -a -m 'added new benchmarks' //git commit 加上 -a 选项，Git 就会自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过 git add 步骤
```
#### 移除文件
* 从工作目录中手工删除文件，需要再运行 git add
* 用命令行删除
```js
$ git rm PROJECTS.md
// 如果删除之前修改过并且已经放到暂存区域的话，则必须要用强制删除选项 -f（译注：即 force 的首字母）
$ git rm --cached README // 让文件保留在磁盘，但是并不想让 Git 继续跟踪。git rm 命令后面可以列出文件或者目录的名字，也可以使用 glob 模式。
```
#### 移动文件
```js
$ git mv file_from file_to // 实现文件的改名
```
#### 查看提交历史
```js
$ git log 
$ git log -p -2 // 一个常用的选项是 -p，用来显示每次提交的内容差异。 你也可以加上 -2 来仅显示最近两次提交。
$ git log --stat // 如果你想看到每次提交的简略的统计信息，你可以使用 --stat 选项。--stat 选项在每次提交的下面列出所有被修改过的文件、有多少文件被修改了以及被修改过的文件的哪些行被移除或是添加了
$ git log --pretty=oneline// 另外一个常用的选项是 --pretty。 这个选项可以指定使用不同于默认格式的方式展示提交历史。 这个选项有一些内建的子选项供你使用。 比如用 oneline 将每个提交放在一行显示，查看的提交数很大时非常有用。 另外还有 short，full 和 fuller 可以用，展示的信息或多或少有些不同。
$ git log --pretty=format:"%h - %an, %ar : %s" // 但最有意思的是 format，可以定制要显示的记录格式。
// 当 oneline 或 format 与另一个 log 选项 --graph 结合使用时尤其有用。 这个选项添加了一些ASCII字符串来形象地展示你的分支、合并历史：
```
#### 撤消操作
* 有时候我们提交完了才发现漏掉了几个文件没有添加，或者提交信息写错了。运行以下命令：
```js
$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend
```
最终你只会有一个提交 - 第二次提交将代替第一次提交的结果。
* 取消暂存的文件
```js
$ git reset HEAD CONTRIBUTING.md 
// 虽然在调用时加上 --hard 选项可以令 git reset 成为一个危险的命令（译注：可能导致工作目录中所有当前进度丢失！），但本例中工作目录内的文件并不会被修改。 不加选项地调用 git reset 并不危险 — 它只会修改暂存区域。
```
* 撤消对文件的修改
```js
$ git checkout -- [file]
// 你需要知道 git checkout -- [file] 是一个危险的命令，这很重要。 你对那个文件做的任何修改都会消失 - 你只是拷贝了另一个文件来覆盖它。 除非你确实清楚不想要那个文件了，否则不要使用这个命令。
```
#### 查看远程仓库
```js
$ git remote //  origin 是 Git 给你克隆的仓库服务器的默认名字
$ git remote -v // 会显示需要读写远程仓库使用的 Git 保存的简写与其对应的 URL。
```
#### 添加远程仓库
```js
$ git remote add <shortname> <url> // 添加一个新的远程 Git 仓库，同时指定一个你可以轻松引用的简写。
```


