# Project 06 — systemd Services (pavitra)

## What I did as teammate
- Tested service management with restricted sudo
- Verified I could start/stop/restart webserver but NOT sshd or others
- Created port conflict by running manual python server on 8080
- Watched bharath diagnose with ss -tlnp and journalctl
- Reported "website down" for each break scenario

## What I learned
- systemctl status shows state and last log lines — no sudo needed to read
- sudo -l shows exactly what I'm allowed to do before trying
- Port conflicts show up clearly with ss -tlnp — always check this first
- The service env file is read-only to me (640, root:webserver) — correct
- journalctl -u webserver -f lets me watch logs live as bharath fixes things

## Commands I now know confidently
systemctl status / is-active / is-enabled
journalctl -u service -b -f --no-pager
ss -tlnp | grep PORT
sudo -l
