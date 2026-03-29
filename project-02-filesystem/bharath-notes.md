# Project 02 — Filesystem & Disks (bharath)

## Setup
- bharath = Terminal 1 (main)
- pavitra = Terminal 2 (SSH via localhost)
- Virtual disk: /srv/virtual-disk.img → /dev/loopX → /mnt/project-data

## What I built
- Explored live filesystem: findmnt, lsblk -f, stat, /proc virtual files
- Created 100MB loop device from image file (dd + losetup)
- Formatted with ext4 (mkfs.ext4 -L)
- Mounted to /mnt/project-data
- Added to /etc/fstab with UUID and nofail option
- Tested fstab: findmnt --verify + mount -a BEFORE trusting it

## Break/fix exercises
1. Disk full (100% Use%):
   → df -h showed full → du -sh sorted by size → found bigfile → rm it
   → Key: if still full after rm, check lsof | grep deleted

2. Bad fstab entry (typo in mount point):
   → findmnt --verify caught it BEFORE reboot
   → mount -a showed the error cleanly
   → Fixed typo, verified again — never rebooted with broken fstab

3. Inode exhaustion (100% IUse% but disk space free):
   → df -h showed space available — confusing
   → df -i showed IUse%=100% — the real problem
   → find to locate directory with most files → rm -rf cache/
   → Key: always check df -i when "no space" but df -h shows free space

## Senior mindset
- Read before write: findmnt + df -h + lsblk before touching anything
- Always back up /etc/fstab before editing
- ALWAYS test fstab: findmnt --verify + mount -a before reboot
- Use UUID not /dev/sdX in fstab — device names change, UUIDs don't
- Two types of "disk full": space (df -h) and inodes (df -i) — check both
- Deleted file space not freed if process holds it open (lsof | grep deleted)
