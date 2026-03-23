# Project 06 — systemd Services (bharath)

## What I built
- System user: webserver (nologin, no home dir)
- App: /srv/webserver/app.py — Python HTTP server
- Unit file: /etc/systemd/system/webserver.service
- Env file: /etc/webserver/env (640 permissions, secrets safe)
- Hardened with 13 security directives — score <4.0

## Team simulation
- Pavitra given restricted sudo: only webserver start/stop/restart/reload/status
- She cannot systemctl anything else — least privilege enforced

## Break/fix exercises
1. Wrong ExecStart path (/usr/bin/python not /usr/bin/python3)
   → journalctl: "No such file or directory" → fixed path with which python3

2. Bad env var (PORT=notanumber → ValueError on startup → restart loop)
   → journalctl: traceback showed ValueError in int() → fixed env file
   → Key: EnvironmentFile changes don't need daemon-reload

3. Port conflict (pavitra's manual server occupying 8080)
   → journalctl: "Address already in use" → ss -tlnp found PID
   → killed the intruder → service started cleanly

## Senior mindset
- ALWAYS: daemon-reload → restart (never just restart after unit file edit)
- enable ≠ start: enable is for boot, start is for now
- Read journalctl BEFORE restarting — logs from the crash are precious
- Test app manually as the service user BEFORE writing the unit file
- Harden iteratively — add directives, test, check score, repeat
- systemd-analyze security shows exactly what's wrong and how to fix it
