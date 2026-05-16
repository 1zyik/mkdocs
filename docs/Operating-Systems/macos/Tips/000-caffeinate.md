---
title: Keep Screen On with Caffeinate
description: How to prevent macOS from sleeping or turning off the display using the built-in caffeinate command.
---

# Keep Screen On with Caffeinate

macOS will dim and turn off the display after a period of inactivity based on your energy settings. In situations where you need the screen to stay on — running a long process, monitoring output, or presenting — you can use the built-in `caffeinate` command to prevent this without touching system preferences.

## The Command

```bash
caffeinate -d
```

The `-d` flag specifically prevents the display from sleeping. The command runs until you stop it with `CTRL+C`.

### Flag Breakdown

| Flag | Effect |
|---|---|
| `-d` | Prevents the display from sleeping |
| `-i` | Prevents the system from idle sleeping |
| `-s` | Prevents the system from sleeping when on AC power |
| `-t <seconds>` | Runs caffeinate for a set duration then exits |

??? Tip
    Flags can be combined. Use `caffeinate -di` to keep both the display and system awake. <br>
    Use `-t` to avoid having to remember to `CTRL+C` when done.

## Running for a Set Duration

```bash
caffeinate -d -t 3600
```

This keeps the display on for exactly one hour (3600 seconds) before caffeinate exits automatically.

## Tying it to Another Process

You can bind `caffeinate` to another command so it stays active only for as long as that process is running:

```bash
caffeinate -d -i <command>
```

```bash
# Example: keep awake while a script runs
caffeinate -d -i ./long-running-script.sh
```

Once the script finishes, `caffeinate` exits automatically.
