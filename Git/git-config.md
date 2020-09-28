# Git Config

## 设置全局配置

```git
git config --global user.name "doun"
git config --global user.email "iamdonydou@gmail.com"
```
## 使用ssh代替https

```git
git config --global url.git@github.com:.insteadOf https://github.com
```

## 查看
```bash
cat ~/.gitconfig
```
或
```git
# system 系统级别
# global 用户级别
# local 当前仓库
git config --global  --list
```

## 忽略文件权限变更

```git
git config core.filemode false
```

## 忽略大小写

```git
git config core.ignorecase false
```