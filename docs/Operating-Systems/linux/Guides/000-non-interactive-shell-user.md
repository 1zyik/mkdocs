---
title: Creating a Non-Interactive Shell User
description: How to create a user account in Linux that cannot be used for interactive login, often for service accounts.
---

# How to Create a Non-Interactive Shell User in Linux

There are times when you need to create a user account on a Linux system that should not have the ability to log in to a shell. These are often called "service accounts" and are used to run applications or services.

Assigning a non-interactive shell to these users is a security best practice. It prevents the account from being used for an interactive session, reducing the potential attack surface.

## The Command

The most common way to create a non-interactive user is with the `useradd` (or `adduser`) command, specifying `/usr/sbin/nologin` as the shell.

```bash
sudo useradd -r -s /usr/sbin/nologin <username>
```

### Command Breakdown

*   `sudo`: The command needs to be run with root privileges.
*   `useradd`: The standard command for adding a new user.
*   `-r`: This flag creates a "system" user. System users are not typically intended for interactive use and often have UIDs in a lower range.
*   `-s /usr/sbin/nologin`: This is the key part. The `-s` flag specifies the user's login shell. `/usr/sbin/nologin` is a special shell that politely refuses a login.
*   `<username>`: Replace this with the desired username for your service account (e.g., `prometheus`, `webapp`).

## Verification

You can verify that the user has been created with the correct shell by checking the `/etc/passwd` file.

```bash
grep <username> /etc/passwd
```

The output should look something like this, with `/usr/sbin/nologin` at the end of the line:

```
<username>:x:999:999::/home/<username>:/usr/sbin/nologin
```

### What Happens if They Try to Log In?

If someone attempts to log in (e.g., via SSH) as this user, their session will be immediately terminated, and they will often see a message like: `This account is currently not available.`