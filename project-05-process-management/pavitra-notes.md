# Project 05 — Process Management (pavitra)

## What I did as teammate
- Started stress processes for bharath to find and kill
- Ran python3 SIGTERM-ignoring process — watched bharath escalate to -9
- Created zombie process — watched that kill -9 failed, parent kill worked
- Tested nohup: closed SSH session, reconnected, process was still alive

## Commands I now know
- jobs, fg, bg, Ctrl+Z workflow
- nohup command &  → survives disconnect
- disown %N        → remove from job table after starting
- pgrep -u me -a   → see all my own processes cleanly

## Key insight
As a developer/user on a shared server:
- Use nice +15 for any heavy jobs — be a good citizen
- nohup everything you want to keep alive through disconnects
- Check jobs before closing terminal — don't orphan processes accidentally
