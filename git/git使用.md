# Git 使用





## 一、配置



### 1、初始配置



```sh
# --global 全局设置 ～/.gitconfig
# 无--global 当前仓库 .git/config

git config --global user.email "email"
git config --global user.name "name"

```





### 2、代理配置



```sh
# 设置代理
git config --global http.proxy http://127.0.0.1:1080
git config --global https.proxy https://127.0.0.1:1080

# 取消代理
git config --global --unset http.proxy
git config --global --unset https.proxy
```



### 3、github ssh



```sh
ssh-keygen -t rsa
```



**将公钥添加至github**





### 4 、配置别名



**1.~/.gitconfig**



```ini
[alias]
	a = add .
	c = commit
	s = status
	l = log
	b = branch

```



**2.系统 ～/.zshrc**



```ini
alias gs="git status"
alias gc="git commit -m "
alias gl="git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
alias gb="git branch"
alias ga="git add -A"
alias go="git checkout"
alias gp="git push;git push github"

```



### 5、git status 不显示中文



```sh
git config --global core.quotepath false
```

