# Git Commands

## 创建本地仓库并关联远程

```
git init
git add .
git commit -m "init"
git remote add origin https://github.com/itisbean/go_learn.git
git push -u origin master
```

## 强制pull

```
git fetch --all
git reset --hard origin/master
git pull
```