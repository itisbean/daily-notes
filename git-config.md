# Git Config

## 设置全局配置

```
git config --global user.name "doun"
git config --global user.email "iamdonydou@gmail.com"
```
## 使用ssh代替https

```
git config --global url.git@github.com:.insteadOf https://github.com
```

## 查看
```
cat ~/.gitconfig
```

## 忽略文件权限变更

```
git config core.filemode false
```