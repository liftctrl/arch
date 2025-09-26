# v2RayA

---

## 1. Prepare Directories

Create project directories:

```bash
mkdir -p software/v2raya/data
```

Create the Docker Compose file:

```bash
nvim software/v2raya/docker-compose.yml
```

## 2. Docker Compose Configuration

Example `docker-compose.yml`:

```yaml
services:
  v2raya:
    image: mzz2017/v2raya:v2.2.5.8
    restart: always
    privileged: true
    network_mode: host
    container_name: v2raya
    environment:
      V2RAYA_LOG_FILE: /tmp/v2raya.log
      V2RAYA_V2RAY_BIN: /usr/local/bin/xray
      V2RAYA_NFTABLES_SUPPORT: off
      IPTABLES_MODE: legacy
    volumes:
      - /lib/modules:/lib/modules:ro
      - /etc/resolv.conf:/etc/resolv.conf
      - $PWD/data:/etc/v2raya
      - /etc/timezone:/etc/timezone:ro
      - /etc/localtime:/etc/localtime:ro
```

## 3. Start the Container

```bash
cd software/v2raya
docker-compose up -d
```

Verify:

```bash
docker ps | grep v2raya
```

---
