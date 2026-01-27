---
title: Creating a Temporary Shell User
description: How to create a user account in Linux that automatically expires after a specific date.
---

# How to Create a Temporary Shell User in Linux

In scenarios involving contractors, temporary employees, or short-term projects, you may need to grant system access for a limited time. Instead of relying on memory to manually disable or delete the account later, Linux allows you to set an automatic expiration date when creating the user.

This ensures that access is revoked automatically, maintaining security hygiene.

## The Command

You can specify an expiration date using the `-e` (or `--expiredate`) flag with the `useradd` command. The date format is typically `YYYY-MM-DD`.

```bash
sudo useradd -e 2024-12-31 <username>
```

### Command Breakdown

*   `sudo`: The command needs to be run with root privileges.
*   `useradd`: The standard command for adding a new user.
*   `-e 2026-12-31`: This flag sets the account expiration date. After this date, the user will no longer be able to log in.
*   `<username>`: Replace this with the desired username (e.g., `contractor_bob`).

## Verification

To verify the account expiration settings, you can use the `chage` command with the `-l` (list) flag.

```bash
sudo chage -l <username>
```

The output will show the "Account expires" field:

```
Account expires						: Dec 31, 2026
```

## Modifying an Existing User

If you have an existing user and want to add or change their expiration date, you can use the `usermod` or `chage` command.

```bash
sudo usermod -e 2024-12-31 <username>
```
