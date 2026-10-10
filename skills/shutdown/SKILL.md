---
name: shutdown
description: Shut the computer down once every other task in the session is finished. For long unattended sessions while the user sleeps.
disable-model-invocation: true
---

The user is asleep and not coming back to this session tonight. The shutdown is the last action of the session, queued behind everything else they asked for.

1. Finish every other task. Push only when the user asked for it, for example with a queued `/push`. Otherwise finished work stays local. A task you cannot finish ends as a written-up blocker, not a question: nobody is awake to answer one.
2. Wait for background work you started (subagents, workflows, background commands) to complete. Nothing still running gets killed by the shutdown.
3. Write the final report now, before the shutdown: what got done, what is blocked and why, what the user should look at first. It is the first thing they read in the morning.
4. Shut down with the command for this host:

| Host | Detect | Command |
|---|---|---|
| WSL | `$WSL_DISTRO_NAME` is set | `powershell.exe -NoProfile -Command "Stop-Computer -Force"` |
| macOS | `uname` is `Darwin` | `osascript -e 'tell application "System Events" to shut down'` |
| Linux | otherwise | `systemctl poweroff` |

On WSL, `shutdown` or `wsl --shutdown` only stops the Linux VM and leaves the Windows host running all night, so the shutdown goes through PowerShell to Windows itself. `-Force` keeps an open Windows app from blocking it at a "save changes?" dialog.

If the command fails or asks for a password, add that to the report and stop. A sudo prompt at night has nobody to answer it.
