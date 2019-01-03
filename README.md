
[Reference](https://www.jianshu.com/p/0984af46f4ec)

## 环境预备

master 分支
```
touch cherry-pick.txt
git add .
git commit -m "create cherry-pick.txt, first commit"
```

develop 分支
```
gco -b develop

touch cherry1.txt
git commit -a -m "cherry 1"

git commit -i -m "cherry 1"
git add .
git commit -m "cherry 1"

touch cherry2.txt
git add .
git commit -m "cherry 2"

touch cherry3.txt
git add .
git commit -m "cherry 3"
```

log
```
git log develop
```

```
commit 79c31c4809fb92c7c236ef10c3fb1049537a8ba6 (develop)
Author: LiYanLance <leeyanly@163.com>
Date:   Thu Jan 3 22:34:00 2019 +0800

    cherry 3

commit 8ceb23250f7a8bec3235ed3b5f897ae8413061be
Author: LiYanLance <leeyanly@163.com>
Date:   Thu Jan 3 22:33:15 2019 +0800

    cherry 2

commit ff239c823878cc5b0d67574c1119a5fb502694e1
Author: LiYanLance <leeyanly@163.com>
Date:   Thu Jan 3 22:32:39 2019 +0800

    cherry 1

commit 65f7a242b89960b97931e7b07acee256b4718fe8 (HEAD -> master)
Author: LiYanLance <leeyanly@163.com>
Date:   Thu Jan 3 22:30:48 2019 +0800

    create cherry-pick.txt, first commit
```

## cherry-pick 操作

### 把 develop 分支的 cherry 3 commit(79c31c) 提交到 master

#### 方法1
```
// 切换到 master 分支
git checkout master
// 挑选提交
git cherry-pick 79c31c
```

git log
```
commit e9c82597eaa97acd62b66b13ffa7db8524903717 (HEAD -> master)
Author: LiYanLance <leeyanly@163.com>
Date:   Thu Jan 3 22:34:00 2019 +0800

    cherry 3

commit 65f7a242b89960b97931e7b07acee256b4718fe8
Author: LiYanLance <leeyanly@163.com>
Date:   Thu Jan 3 22:30:48 2019 +0800

    create cherry-pick.txt, first commit
```

但是通过 git log 可以看到, cherr3 和 master 当前这个不是一个提交, commit 标号不一样.


#### 方法 2

挑选 branch 最顶端的提交
git cherry-pick branch-name

```
git cherry-pick develop
```

### 把 develop 分支的 cherry 3 和 1 先后提交到 master

提交多个 commit
git cherry-pick commit3 commit1

```
gco master
git cherry-pick 79c31c ff239c
```


### 把 develop 的 2 - 3 都提交到 master

git cherry-pick commit1..commit3  左开右闭区间

git cherry-pick commit2^..commit3 封闭区间

```
git cherry-pick ff239c..79c31c
```