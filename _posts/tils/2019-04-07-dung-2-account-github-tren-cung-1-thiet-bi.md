---
layout: tils_layout
title:  "Dùng 2 account github trên cùng 1 thiết bị"
author: sondh5
categories: [ TILs, Git ]
status: public
---

Config lại file `~/.ssh/config`

```ruby
# Account của công ty
Host github.com
HostName github.com
User git
IdentityFile ~/.ssh/id_rsa

# Account cá nhân
Host github-me
HostName github.com
User git
IdentityFile ~/.ssh/id_rsa_me
```

Khi Clone thì chú ý url, sửa `git@github.com` thành `git@github-me`
```
git clone git@github-me:account_name/repo_name.git

```

Check lại remote:
```
git remote -v
origin	git@github-me:account_name/repo_name.git (fetch)
origin	git@github-me:account_name/repo_name.git (push)
```

##### Config author
- Add config system
```ruby
# /etc/gitconfig
[user]
   email = account@company.com
   name = company
```
- Add config local
```ruby
# your_personal_repo/.git/config
[user]
   email = account@me.com
   name = me
```