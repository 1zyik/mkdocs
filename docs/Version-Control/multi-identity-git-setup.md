---
title: Multi-Identity Git & SSH Setup
description: How to manage multiple Git identities (personal, work) on a single machine using conditional includes and SSH host aliases.
icon: material/account-key
---

# Multi-Identity Git & SSH Setup

When working across multiple GitHub accounts — for example, personal projects and a work organisation — you need Git to automatically apply the correct identity (name, email, signing key) and SSH to use the correct authentication key, depending on which repo you're in.

This guide documents the approach used here: workspace-based directory separation, Git conditional includes, and SSH host aliases.

---

## Overview

The setup is built around three files working together:

| File | Role |
|---|---|
| `~/.gitconfig` | Global Git config — sets signing format and routes to identity configs |
| `~/.config/git-configs/.gitconfig-*` | Per-identity configs (user, email, signing key) |
| `~/.ssh/config` | SSH host aliases — maps each identity to its own auth key |

Each identity also has two SSH keys:

- An **auth key** — used for push/pull over SSH
- A **signing key** — used to sign commits via `gpg.format = ssh`

---

## Directory Layout

Repos are organised into top-level workspace folders under `~/repos/`. Git conditional includes use these paths to automatically select the right identity.

```
~/repos/
├── 01-personal/     ← personal identity applied here
└── 02-work/         ← work identity applied here
```

---

## `~/.gitconfig` — Global Config

```ini
[gpg]
    format = ssh

[includeIf "gitdir:~/repos/01-personal/"]
    path = ~/.config/git-configs/.gitconfig-personal

[includeIf "gitdir:~/repos/02-work/"]
    path = ~/.config/git-configs/.gitconfig-work
```

**`gpg.format = ssh`** tells Git to use SSH keys for commit signing instead of GPG keys. This is set globally so it applies regardless of which identity is active.

The `includeIf` directives conditionally load an identity config based on where the repo lives. Git matches the `gitdir:` path against the repo's `.git` directory location — if it matches, the referenced config file is merged in.

!!! info "Trailing slash matters"
    The trailing `/` on `gitdir:~/repos/01-personal/` ensures the match applies to any repo *inside* that directory, not just the directory itself.

---

## Per-Identity Configs

### Personal — `~/.config/git-configs/.gitconfig-personal`

```ini
[user]
    name = your-username
    email = you@personal-email.com
    signingkey = ~/.ssh/personal_github_sign.pub

[commit]
    gpgsign = true

[gpg]
    format = ssh
```

### Work — `~/.config/git-configs/.gitconfig-work`

```ini
[user]
    name = your-work-username
    email = you@work-email.com
    signingkey = ~/.ssh/work_github_sign.pub

[commit]
    gpgsign = true

[gpg]
    format = ssh
```

Each config sets the `user.name`, `user.email`, and `user.signingkey` for that identity. Setting `commit.gpgsign = true` means every commit in repos under that workspace is automatically signed — no flags required.

---

## `~/.ssh/config` — SSH Host Aliases

```ssh-config
# Personal GitHub
Host github.com-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/personal_github
    IdentitiesOnly yes

# Work GitHub
Host github.com-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/work_github
    IdentitiesOnly yes
```

Both aliases resolve to `github.com` but each presents a different SSH key. `IdentitiesOnly yes` prevents SSH from offering any other loaded keys (e.g. from `ssh-agent`), ensuring the right key is always used.

!!! warning "Remote URLs must use the alias"
    For SSH auth to route correctly, the remote URL in each repo must reference the alias, not the bare `github.com` hostname.

    ```bash
    # Personal repo
    git remote set-url origin git@github.com-personal:your-username/my-repo.git

    # Work repo
    git remote set-url origin git@github.com-work:your-work-org/my-repo.git
    ```

---

## SSH Keys Summary

| Identity | Auth Key | Signing Key |
|---|---|---|
| Personal | `~/.ssh/personal_github` | `~/.ssh/personal_github_sign.pub` |
| Work | `~/.ssh/work_github` | `~/.ssh/work_github_sign.pub` |

Auth keys are registered as **SSH keys** on the GitHub account. Signing keys are registered as **Signing keys** on the GitHub account — this is what allows GitHub to display the "Verified" badge on commits.

---

## Verifying the Setup

### Check which identity Git will use in a given repo

```bash
git config user.name
git config user.email
git config user.signingkey
```

Run these from inside a repo and confirm the values match the expected identity for that workspace.

### Test SSH auth for each alias

```bash
ssh -T git@github.com-personal
ssh -T git@github.com-work
```

A successful connection returns something like: `Hi your-username! You've successfully authenticated...`

### Confirm commit signing works

```bash
git log --show-signature -1
```

Look for `Good "git" signature` in the output.
