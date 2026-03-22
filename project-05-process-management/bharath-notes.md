# Project 05 — Process Management (bharath)

## What I practised
- ps aux, ps auxf, ps -eo with custom columns
- pgrep to find processes without grep
- top: P=sort CPU, u=filter user, k=kill, r=renice, 1=per-core
- htop: F5 tree view, F9 signal menu, F3 search
- kill with SIGTERM first, then SIGKILL if needed
- pkill to kill by name, renice to change running process priority
- nohup + & for processes that survive SSH disconnect
- /proc/PID/ exploration: cmdline, status, exe, fd
- Created and fixed a zombie: kill parent, not zombie

## Break/fix exercises
1. Rogue CPU process: found with top/ps, identified via /proc, killed with SIGTERM
2. SIGTERM-ignoring process: escalated to SIGKILL after SIGTERM failed
3. Zombie process: kill -9 failed, killed parent instead, systemd cleaned up

## Senior mindset learned
- Load avg > nproc = overloaded. Always check nproc first.
- Read /proc before killing — know what you're terminating
- SIGTERM → wait → SIGKILL. Never start with -9.
- D state (uninterruptible sleep) cannot be kill -9'd. Fix the I/O.
- Zombie = dead child with uncollected exit status. Fix the parent.
- nohup + disown = process survives disconnect. Different tools, same goal.
