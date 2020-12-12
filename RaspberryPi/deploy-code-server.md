# Deploy Code-server on Raspberry Pi OS (version 10)

https://github.com/cdr/code-server

## Upgrade NodeJS
```bash
sudo npm cache clean -f
sudo npm install -g n
sudo n stable
```

## Dependencies
```bash
sudo apt install xkbfile libx11-dev libxkbfile-dev libsecret-1-dev
```

## Install Script
```bash
curl -fsSL https://code-server.dev/install.sh | sh
```
