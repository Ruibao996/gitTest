# Git

## 基本指令

1. cd 进入到文件夹~
2. cd .. 进入到上一级（cd与点中间有一个空格）
3. pwd 显示当前目录路径
4. ~ 表示当前用户下
5. ls(ll)  都是列出当前目录下的所有路径，ll可以可以列出.开头的隐藏文件
6. touch 新建一个文件（在当前目录下）
7. rm 删除一个文件
8. mkdir 新建一个目录即文件夹, 后面直接跟文件名
9. rm -r 删除一个文件夹，mr -r src 就是删除叫src的目录
10. mv 移动文件，mv index.html src，index.html 是要被移动的文件，src是目标文件夹，这样写必须保证文件和目标文件在同一目录下
11. reset 清屏，将git bash 命令窗口的所有内容清空
12. cat 查看当前文件实时修改内容
13. 后面要接双引号时前面要打个空格

## 建立仓库和修改其中文件

**每次修改和创建都需要重新添加(add)和提交(commit)**

1. 建立仓库：git init

2. 查看文件状况（整个文件夹内的）git status

3. 将工作区(workspace)转移到暂存区(index) git add 文件名

4. 通用的话(全部文件) git add .

5. 将暂存区(index)提交到仓库(repository) git commit -m "版本名"

6. 察看仓库 git log

7. vi 可以编辑文件

8. 在vi界面内下方:wq可以退出编辑

9. 版本切换 git reset --hard commitID

    *commitID 可以使用`git-log`或者`git log`指令查看*

   切换的时候用`git reflog`可以看所有的commitID

10. 查看已经删除的提交记录 git reflog

11. 不想让git管理目录下的部分文件时，可以创建名为`.gitignore`的文件

    ```git
    RuiBaby@▒𱦵Ļ▒˶ MINGW64 ~/Desktop/gitTest (master)
    $ touch file02.a
    
    RuiBaby@▒𱦵Ļ▒˶ MINGW64 ~/Desktop/gitTest (master)
    $ touch .gitignore
    
    RuiBaby@▒𱦵Ļ▒˶ MINGW64 ~/Desktop/gitTest (master)
    $ vi .gitignore
    ```

    修改.gitignore界面 

    ```vi
    *.a
    ```

    这个例子避免.a结尾的文件被git操作

## 分支操作

将工作从开发主线分离开进行重大的bug修复，开发新的功能，以免影响开发主线

主要 分支+合并

1. 查看分支 git branch

2. 创建新分支 git branch 分支名

3. `98718a4 (HEAD -> master, dev01) update file01`HEAD所指表明在哪个分支上进行操作

4. 切换分支 git checkout 想切换到的分支名

5. 创建分支并切换 git checkout -b

6. 删除分支 git branch -d

   强制删除 git branch -D

7. 合并分支(将想要合并的分支合并到现在的head所指) git merge 想和并分支

## 解决冲突

**问题背景：**在不同分支修改相同文件且修改的内容不同

```git
RuiBaby@▒𱦵Ļ▒˶ MINGW64 ~/Desktop/gitTest (master)
$ git merge dev
Auto-merging file01.txt
CONFLICT (content): Merge conflict in file01.txt
Automatic merge failed; fix conflicts and then commit the result.

RuiBaby@▒𱦵Ļ▒˶ MINGW64 ~/Desktop/gitTest (master|MERGING)
$ vi file01.txt
```

现在所表现的vim界面

```vim
<<<<<<< HEAD
update count=03
=======
update count=02
>>>>>>> dev
```

需要删掉，只保留想显示的内容

```vim
update count=02
```

然后直接`git add .`

再`git commit`

## 远程仓库

1. 生成SSH公钥 ssh-key -t rsa

   不断回车，如果公钥存在则自动覆盖

2. 获取公钥 cat ~/.ssh/id_rsa.pub

3. 验证是否配置成功 ssh -T 

4. 添加远程仓库

   git remote add <远程名称> <仓库路径>

   仓库路径，从远端服务器获取此URL

   ```git
   RuiBaby@▒𱦵Ļ▒˶ MINGW64 ~/Desktop/gitTest (master)
   $ git remote add origin git@github.com:Ruibao996/gitTest.git
   ```

5. 查看远程仓库 git remote

6. 推送至远程仓库 git push [-f] [--set-upstream] [远端名称 [本地分支名] [:远端分支名]] 如 git push origin master:master

   -f 表示强行覆盖，--set-upstream表示推送到远端的同时并且建立起和远端分支的关联关系

   如果远程分支名和本地分支名称相同，则可以指写本地分支 git push origin master

## clone

1. git clone 仓库路径 目录名称

## 抓取和拉取

1. 抓取：git fetch [remote name] [branch name] 

   抓取指令将仓库更新都抓取到本地，不会进行合并

   如果不指定远端名称和分支名，则抓取所有分支

2. 拉取：git pull [remote name] [branch name]

   拉取指令将远端仓库修改拉到本地并自动进行合并，等同于fetch+merge

   如果不指定远端名称和分支名，则抓取所有并更新当前分支

## 解决远程冲突![屏幕截图 2023-08-04 163336](C:\Users\Rui\Desktop\gitTest\testDir\屏幕截图 2023-08-04 163336.png)

