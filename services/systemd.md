# systemd Services Configuration

---

## 1. Boot Optimization

Check which services delay boot:

```bash
systemd-analyze blame
```

A common delay source is `systemd-networkd-wait-online`. You have two options:

**Option 1: Disable globally**

```bash
sudo systemctl disable systemd-networkd-wait-online.service
```

**Option 2: Wait only for a specific interface**

```bash
sudo systemctl edit systemd-networkd-wait-online.service
```

Add:

```ini
[Service]
ExecStart=
ExecStart=/usr/lib/systemd/systemd-networkd-wait-online \
  --interface=wlp2s0 --timeout=30
```

> ⚠️ Disabling wait-online may affect services that require a fully initialized network.

---

## 2. systemd-networkd

**DHCP Configuration**

Create `/etc/systemd/network/20-dhcp.network`:

```ini
[Match]
Name=*

[Network]
DHCP=yes
LinkLocalAddressing=no
IPv6AcceptRA=no
```

**Static IP Configuration**

Create `/etc/systemd/network/30-static.network`:

```ini
[Match]
Name=*

[Network]
Address=192.168.1.100/24
Gateway=192.168.1.1
DNS=8.8.8.8
LinkLocalAddressing=no
IPv6AcceptRA=no
```

**Wi-Fi Setup**

1. Generate WPA config:

```bash
sudo wpa_passphrase "YourSSID" "YourPassword" | \
  sudo tee /etc/wpa_supplicant/wpa_supplicant-wlp2s0.conf
```

2. Enable services:

```bash
sudo systemctl enable --now wpa_supplicant@wlp2s0.service
sudo systemctl enable --now systemd-networkd
```

**Verification**

```bash
networkctl status
```

---

## 3. systemd-resolved

Enable and start the service:

```bash
sudo systemctl enable --now systemd-resolved
```

Link `resolv.conf`:

```bash
sudo ln -sf /run/systemd/resolve/stub-resolv.conf /etc/resolv.conf
```

Check DNS resolution:

```bash
resolvectl status
```

---
