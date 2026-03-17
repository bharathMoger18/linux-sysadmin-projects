# Project 01 — Pavitra's notes

## What I tested as teammate
- SSH'd into localhost as pavitra
- Verified webteam group membership with id
- Created files in /mnt/linux_projects/shared — confirmed webteam group inherited
- Tested file access: public (yes), team (yes), private (no)
- Verified restricted sudo: apt/systemctl/git work, useradd denied
- Hit all 3 break scenarios and watched bharath fix them

## What I learned
- sudo -l is the first thing to run when you don't know your own access
- Permission denied on cd = missing execute bit, not read
- Being in a group doesn't help if you haven't re-logged in
