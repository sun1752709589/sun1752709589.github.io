---
layout: post
title: Ubuntu系统autojump使用
---

Ubuntu系统autojump使用

### Ubuntu系统autojump使用
```
install:
sudo apt-get install autojump
add one path:
autojump -a /you/path
show autojump db:
autojump -s
```
### Ubuntu安装完注意事项
```
Debian testing/unstable, Ubuntu, Linux Mint

All Debian-derived distros require manual activation for policy reasons, please see /usr/share/doc/autojump/README.Debian.

To use autojump, you need to configure you shell to source
/usr/share/autojump/autojump.sh on startup.

If you use Bash, add the following line to your ~/.bashrc (for non-login
interactive shells) and your ~/.bash_profile (for login shells):
. /usr/share/autojump/autojump.sh

If you use Zsh, add the following line to your ~/.zshrc (for all interactive shells):
. /usr/share/autojump/autojump.sh
```
