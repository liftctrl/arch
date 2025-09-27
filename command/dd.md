# dd Command Notes

This document collects useful `dd` commands for daily work.

---

## 1. Create Bootable USB

Write an ISO to a USB device:

```bash
sudo dd if=archlinux-2025.iso of=/dev/sdX bs=4M status=progress oflag=sync
```

### 1.1 Notes

- if → input ISO file
- of → target USB device (e.g., /dev/sdb)
- bs=4M → block size
- status=progress → show progress
- oflag=sync → ensure all data is written

> ⚠️ Double-check of=. Wrong device = data loss.

### 1.2 Verify USB

```bash
sudo fdisk -l /dev/sdX
```

Optional:

```bash
sudo mount /dev/sdX1 /mnt
ls /mnt
sudo umount /mnt
```

### 1.3 Flush Writes

```bash
sync
```

---
