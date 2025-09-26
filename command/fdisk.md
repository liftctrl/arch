# fdisk Command Notes

## Format USB

1. **List disks** to identify the target device:

```bash
sudo fdisk -l
```

2. **Start fdisk** on the target device (replace /dev/sdX):

```bash
sudo fdisk /dev/sdX
```

3. **Inside fdisk**, use these commands:

- `o` → create a new empty DOS partition table (erases all data)
- `n` → create a new partition (choose primary, defaults are usually fine)
- `t` → set partition type (optional, e.g., `b` for W95 FAT32)
- `w` → write changes and exit

4. **Format the partition** (usually /dev/sdX1) with a filesystem:

```bash
sudo mkfs.vfat -F 32 /dev/sdX1  # FAT32
# or
sudo mkfs.ext4 /dev/sdX1        # ext4
# or
sudo mkfs.ntfs /dev/sdX1        # NTFS
```

> ⚠️ **Warning**: Double-check the device name `/dev/sdX`. Formatting will erase all data on the device.

Check the new partition table:

```bash
sudo fdisk -l /dev/sdX
```

---
