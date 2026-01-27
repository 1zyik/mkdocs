---
title: Disable Root Login in Linux
description: How to disable root login in Linux.
---

# How to Disable Root Login in Linux

Disabling root login is a critical security measure for any Linux system. It forces all users, including administrators, to log in with their own user account and then elevate their privileges using `sudo`. This creates an audit trail and prevents direct attacks on the root account.

## The Command

The most common way to disable root login is to edit the SSH daemon's configuration file, `/etc/ssh/sshd_config`, and set the `PermitRootLogin` option to `no`.

```bash
sudo vi /etc/ssh/sshd_config
```

Inside the file, find the line that says `PermitRootLogin` and change its value to `no`:

```
PermitRootLogin no
```

If the line is commented out (starts with a `#`), remove the `#` to uncomment it.

## Restart the SSH Service

After saving the changes to the configuration file, you need to restart the SSH service for the changes to take effect.

```bash
sudo systemctl restart sshd
```

## Verification

To verify that root login is disabled, you can try to SSH into the server as the root user from another terminal.

```bash
ssh root@<your_server_ip>
```

You should see a "Permission denied" error.