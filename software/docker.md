# Docker

---

## 1. Docker

Install Docker:

```bash
sudo pacman -S docker
```

Add your user to the Docker group:

```bash
sudo usermod -aG docker $(whoami)
```

Create Docker config directory:

```bash
sudo mkdir -p /etc/docker
```

Create /etc/docker/daemon.json to use a registry mirror:

```bash
cat <<EOF | sudo tee /etc/docker/daemon.json > /dev/null
{
    "registry-mirrors": [
        "https://docker.1panel.live"
    ]
}
EOF
```

Enable and start Docker:

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now docker
```

Verify Docker:

```bash
docker ps
```

---

## 2. Docker Compose

Install Docker Compose:

```bash
sudo pacman -S docker-compose
```

Verify installation:

```bash
docker-compose --version
```

---
