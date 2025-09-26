# dd Command Notes

---

## Create a Bootable USB

Write an ISO to a USB drive:

```bash
sudo dd if=archlinux-2025.xx.xx-x86_64.iso of=/dev/sdX bs=4M status=progress oflag=sync
```

- `if` → input file (ISO image)
- `of` → target USB device (e.g., /dev/sdb)
- `bs=4M` → block size for faster writing
- `status=progress` → show progress during writing
- `oflag=sync` → ensure data is fully written

> ⚠️ **Warning**: Double-check `of=` points to the correct device. Writing to the wrong drive will erase it.

Check partitions:

```bash
sudo fdisk -l /dev/sdX
```

Optionally mount and verify files:

```bash
sudo mount /dev/sdX1 /mnt
ls /mnt
sudo umount /mnt
```

---
