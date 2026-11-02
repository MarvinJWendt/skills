---
name: shutdown
description: Shut the computer down once every other task in the session is finished. For long unattended sessions while the user sleeps.
disable-model-invocation: true
---

The user is asleep and not coming back to this session tonight. The shutdown is the last action of the session, queued behind everything else they asked for.

1. Run the `finish` skill over every other task in the session, through its final report. It covers the unattended work: decisions, git, blockers, waiting for background jobs, and the report the user reads in the morning.
2. Shut down with the command for this host:

| Host | Detect | Command |
|---|---|---|
| WSL | `$WSL_DISTRO_NAME` is set | `powershell.exe -NoProfile -Command "Stop-Computer -Force"` |
| macOS | `uname` is `Darwin` | `osascript -e 'tell application "System Events" to shut down'` |
| Linux | otherwise | `systemctl poweroff` |

On WSL, `shutdown` or `wsl --shutdown` only stops the Linux VM and leaves the Windows host running all night, so the shutdown goes through PowerShell to Windows itself. `-Force` keeps an open Windows app from blocking it at a "save changes?" dialog.

If the command fails or asks for a password, add that to the report and stop. A sudo prompt at night has nobody to answer it.
