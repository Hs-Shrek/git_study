## Git

### 基本使用

- 配置自己的 git
  git config --global user.name "胡爽"
  git config --global user.email "15897666973@163.com"
- 查看自己的 git 配置
  git config --list --global

在终端里面打开文件夹路径

- 1.初始化本地管理
  git init

- 2.将文件添加到暂存区（临时存放代码的位置）【**一般代码做完一部分就添加一次**，也是必须的；】
  git add ./文件 1 路径 ./文件 2 路径  
  git add . 把文件夹里面所有文件的纳入管理

- 3.提交暂存区代码到本地仓库（正式存放的位置）【一般是完成的阶段性任务可以提交一次，形成正式版本】
  git commit -m '初始化版本号'

- 4.查看提交的历史版本
  git log

- 5.查看当前文件的状态
  git status

- 6.提交修改最后一次的备注
  git commit --amend

- 7.文件移出缓存区
  git rm --cached ./文件路径

- 8.查看历史版本的 ID 值
  git log --oneline

- 9.回滚到指定的版本
  git reset --hard ID

- 10.撤销，用暂存区修改前的代码覆盖当前工作目录的代码
  git checkout .

### 四个文件状态

1. 红色的文件名 未纳入 git 文件管理 未 git add
2. new:绿色的文件名 纳入了暂存区的文件名 git add 了
3. 无颜色和文件 已经提交版本号了 git commit -m""了
4. modified:红色的文件名 暂存区的文件被修改了

### 基本流程

- 添加到暂存区：（更新记录的起始点、对比点）

  - 新创建的文件不会被主动管理,需要自己 add；
  - **一般在没有完成阶段性代码的时候，不要重复的对已经管理的文件，再次添加到暂存区；**

- 提交到本地仓库：

  - # 完成了一个阶段性任务的时候就需要 commit
  - 在正式 commit 之前，**必须更新暂存区记录点；`执行 git add .`**
  - # 2.如果当前的文件列表不包含新建的文件，可以 add 和 commit 合并提交
    git commit -a -m "备注"

- 注释细节：

  - git commit --amend 添加或者修改最后一提交的时候的备注
  - 具体步骤：
    1、执行命令 git commit --amend
    2、在打开的窗口中按一下字符 【i】，那么就进入编辑状态（左下角出现插入两个字）
    3、此时就可以修改备注了，修改完成后按一下 【ESC】 按键，退出编辑状态
    4、英文输入法状态下，按 【shift】 和 【: 】 然后左下角出现光标
    5、输入【wq】，然后回车，完成编辑！

  - 提交代码时，不添加-m，那么会强制提示窗口填写备注
    git commit
    1、执行上述命令后，会直接打开添加备注的窗口
    2、按一下 【i】 字符进入编辑状态
    3、输入备注信息，然后按 esc 键退出编辑模式
    4、在英文输入状态下，按 shift + : 然后左下角出现光标
    5、输入【wq】 完成提交

### 版本回滚

- 回滚代码版本
  - 查看历史版本的 ID 值
    git log --oneline
  - 回滚到指定的版本
    git reset --hard ID

```bash
git log --oneline
  a9c88d8 (HEAD -> master) v1测试
  a59c6fe v.0初始化- 修改一下

git reset --hard a59c6fe
```

- 移出暂存区 : 把暂存区的某些文件再撤销到工作目录，那么 git 将不再管理记录该文件！自己就可以手动删除！相当于 git add 的逆操作

  - 把某些文件移出暂存区，移出去后，提交本次仓储时，就不会对该文件进行提交；
    git rm --cached 需要移除文件路径名字
  - 继续提交
    1.  git commit -a -m"备注"
    2.  git add ./非被移除的路径文件
        git commit -m"备注"

- 撤销 : 用暂存区修改前的代码覆盖当前工作目录的代码
  - 没有提交就发小
    git checkout .

## 远程仓库，公共仓库

- 远程公共仓库

  - github
  - 码云

### 【本地】提交到 【github】 流程

- 本地代码初始化，提交 add commit 完成之后，上传到 github

  1. git init
  2. git add README.md
  3. git commit -m "备注"
  4. git branch -M main // 暂时忽略

- 远端新建文件， 名字默认 origin 不改变

  5. git remote add origin https://github.com/hushuang-pangpang/study_demo. (该地址是这个仓库的地址)
  6. git push -u origin main

- 将本地的代码提交到 origin 这个文件内， 提示登录是指 github 的账户

  7. git branch -M main // 暂时忽略
  8. git push -u origin main (-u 是将本地仓储和远程仓储关联，第一次输入，后续可以直接 push)

```bash
  # 修改别名 (把origin修改为其他的名称)
  git remote rename origin 其他
  # 删除别名
  git remote remove origin
  # 查看别名
  git remote -v
```

### 从 【github】 拉取代码到【本地】再开发

- 把远程仓库的代码完整复制一份到本地
  git clone 远程仓库地址
- 已经克隆下来的代码，更新提交只能 git pull
  git pull origin master
  git pull

### 配置 ssh 验证

提交代码时不需要输入帐号密码

- 生成公钥和私钥

```bash
# ssh-keygen -t rsa -C '你的邮箱地址'
ssh-keygen -t rsa -C "425543526@qq.com"
```

- 进入文件夹路径 复制公钥内容
- 进入 github - 个人头像 - settings - SSH and GPG keys - New SSH key - Key 放公钥内容，Title 随便起

### 分支

- 分支：把代码复制一份新的就是一个新的分支（分支就是某一个版本代码的复制品）
  - 测试项目时一般会以某一个分支为基准进行测试（测试分支）
  - 有时代码出现了 bug，此时可以创建一个单独的分支来修复 bug（bug 修复分支）
- 意义：

  - 成型版本；处于主分支 master 分支；
  - 继续开发新的功能的时候 ：一般情况不是在主分支上进行新的开发；
  - 在一个新的分支进行开发；

- 查看所有分支
  git branch
- 创建分支
  git branch 分支名称
  # 1.创建分支时是以当前分支最后一个版本为基准
  # 2.创建出来的分支是一份独立的代码
- 切换分支
  git checkout 分支名称
  # 1.切换分支后，当前工作目录中看到的代码就是新切换的分支的代码
  # 2.切换分支时，需要先提交代码 git commit，就是先定一个版本；
- 创建 + 切换分支  
  git checkout -b 分支名称
- 删除分支
  git branch -d/-D 分支名称

  # 如果 test 分支已经被合并了，那么才可以删除，否则无法删除

  git branch -d test

  # 强制删除分支，无论合并与否都会删除！

  git branch -D test

- 普通合并

  - 前提 ： 合并前所有的分支都需要 commit 一个各自的版本

  - 在当前分支 把其他分支合并过来
    git merge 其他分支名;
  - 把其他分支删除
    git branch -d test
    git branch -D test

- 冲突合并
  - 原因 ：不同分支的 【相同文件的相同位置】 的代码都进行了修改
  - 解决了冲突之后，需要重新提交一个历史版本 git commit -a -m""
