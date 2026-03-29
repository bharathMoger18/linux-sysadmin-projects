# Project 02 — Filesystem (pavitra)

## What I did as teammate
- Explored /proc together — realised it's not real files on disk
- Checked my own project directory size with du
- Wrote files to shared /mnt/project-data — confirmed webteam group inherited
- Ran the inode exhaustion scenario (6100 tiny files in cache/)
- Filled the disk with dd — watched bharath diagnose and recover it
- Watched the fstab break/fix — learned why findmnt --verify saves lives

## Key things I learned
- df -h = how full the filesystem is (space)
- df -i = how full the inode table is (file count limit)
- These are independent — one can be full while other is fine
- lsblk -f shows UUID which goes in fstab — never use /dev/sdX
- Loop devices are just files that act like disks — snaps use this

## Commands I now know
findmnt / findmnt --verify
lsblk -f / blkid
df -h / df -i
du -sh * | sort -rh
stat filename
ls -i filename  (show inode number)
