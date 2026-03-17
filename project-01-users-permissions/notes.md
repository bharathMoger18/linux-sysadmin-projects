# Project 01 — Users, Groups & Permissions

## Setup
- bharath = main user (me)
- pavitra = teammate (SSH via localhost)
- Both on same Ubuntu machine under /mnt/linux_projects/developers/

## What we built
- webteam group — both users added
- /mnt/linux_projects/shared with setgid (2775)
- Files with 644, 660, 600 — tested from both users
- pavitra given restricted sudo: apt, systemctl, git only

## Break/fix exercises
1. Wrong group (bharath:bharath) — diagnosed with ls -la, fixed chown
2. chmod 666 on directory — cannot cd without execute bit, fixed 2775
3. sudoers chmod 640 — sudo broke, recovered with pkexec

## Key commands learned
useradd, usermod -aG, groupadd, groups, id, newgrp
chmod (numeric), chown, stat
visudo, sudo -l, pkexec

## Senior mindset
- Read state before changing anything: id, ls -la, stat
- Group changes need re-login or newgrp to take effect
- Execute bit on directories = permission to enter, not just read names
- sudo -l shows exactly what a user can do — use it constantly
- pkexec is your recovery tool when sudo itself breaks
