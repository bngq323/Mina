# Mina Block Producer Hand Book on Mainnet
## Setup firewall
```bash
sudo ufw allow 22
sudo ufw allow 8302
sudo ufw allow 3085
sudo ufw enable
sudo ufw status
```
## Setup environment
vi ~/.mina-env
```bash
MINA_PUBLIC_KEY="<Your Public Key>"
MINA_PRIVKEY_PASS="<Your Private Key Password>"
LOG_LEVEL=Info
FILE_LOG_LEVEL=Debug
EXTRA_FLAGS=" --block-producer-key /home/dhtvblvo4zge/keys/my-wallet"
```
## Import Private Key file (my-wallet )
```bash
mkdir ~/keys
chmod 700 ~/keys
vi ~/keys/my-wallet
chmod 600 ~/keys/my-wallet 
```
## Install Mina Packages
```bash
sudo rm -rf ~/.mina-config
sudo rm -r /tmp/*
sudo rm /etc/apt/sources.list.d/mina*.list
echo "deb [trusted=yes] http://packages.o1test.net $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/mina.list
sudo apt-get update
sudo apt-get install -y mina-mainnet=1.4.0-c980ba8
mina version
```
## Enable Mina service
```bash
systemctl --user daemon-reload
systemctl --user enable mina
```
## Start Mina
`systemctl --user start mina`
## Check status
```bash
systemctl --user status mina
journalctl --user -u mina -n 1000 -f
```
## Stop Mina
```bash
### reload mina.service
systemctl --user stop mina
sudo rm -rf ~/.mina-config
sudo rm -r /tmp/*
history -c
```
