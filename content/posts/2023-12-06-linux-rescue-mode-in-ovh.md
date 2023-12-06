---
title: Linux Rescue Mode in OVH
date: 2023-12-06T01:31:35.564Z
---
1. Restart in rescue mode via OVH panel
2. Check disk partition

```bash
lsblk
```
will output like this
![](/static/img/disk.png)

2. then mount the partition
```bash
# mkdir /mnt/root
# mount /dev/sda1 /mnt/root
```

3. then change root
```bash
chroot /mnt/root
```