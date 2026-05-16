---
title: Git Tips
description: This doc page covers tips and tricks you can use with Git.
icon: material/git
---

# Git Tips and Tricks

### Delete all local branches except `main/master`
``` bash
git branch | grep -v "main" | xargs git branch -D
```

??? Tip
    Replace main with branch of your choice <br>
    Can be tied with a linux alias to speed up cleanup process

### Verify an SSH key fingerprint
``` bash
ssh-keygen -lf /path/to/your/key.pub
```

??? Tip
    Useful for confirming a key matches what's registered on GitHub. <br>
    Works on both auth keys and signing keys.

### Clone a remote feature branch
``` bash linenums="1"
# Clone repo normally
git clone https://github.com/1zyik/t1nk3r.git

#Fetch latest origin updates
git fetch origin

# Checkout into remote feature branch
git checkout -b {feature-branch-name} origin/{feature-branch-name}
```
!!! Warning
    Intended feature branch should already exist in remote
