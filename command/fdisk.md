# fdisk Command Notes

This document collects useful `fdisk` commands for daily work.

---

## 1. Format USB

### 1.1 List Disks

Identify the target device:

```bash
sudo fdisk -l
```

### 1.2 Start fdisk

Replace `/dev/sdX` with your target device:

```bash
sudo fdisk /dev/sdX
```

### 1.3 fdisk Commands

Inside `fdisk`, use:

- `o` → create a new empty DOS partition table (erases all data)
- `n` → create a new partition (primary, defaults usually fine)
- `t` → set partition type (optional, e.g., b for W95 FAT32)
- `w` → write changes and exit

### 1.4 Format Partition

Usually /dev/sdX1:

```bash
sudo mkfs.vfat -F 32 /dev/sdX1  # FAT32
sudo mkfs.ext4 /dev/sdX1        # ext4
sudo mkfs.ntfs /dev/sdX1        # NTFS
```

> ⚠️ Double-check `/dev/sdX`. Formatting erases all data.

### 1.5 Verify

```bash
sudo fdisk -l /dev/sdX
```

---
