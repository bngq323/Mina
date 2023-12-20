# Mina Block Producer Hand Book on Mainnet
This hand book guides Block Producer how to deploy a mina node which running as a service and how to check node status. 
_Current mina version is mina-mainnet=1.4.0-c980ba8_   
_Chain-id:5f704cc0c82e0ed70e873f0893d7e06f148524e3f0bdae2afb02e7819a0c24d1_   
_Git SHA-1:c980ba87c3417f40a7081225dfe7478c5ee70fd7_   
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
## Stop Mina
```bash
systemctl --user stop mina
sudo rm -rf ~/.mina-config
sudo rm -r /tmp/*
history -c
```
## Check status
```bash
systemctl --user status mina
journalctl --user -u mina -n 1000 -f
```
mina client status
```bash
Mina daemon status
-----------------------------------

Global number of accounts:                     189516
Block height:                                  315309
Max observed block height:                     315309
Max observed unvalidated block height:         315309
Local uptime:                                  33m53s
Ledger Merkle root:                            jxbcWQsASfpN15hybJExFw141agXwVSkrBJy4DC2EhJnf2Td7Uq
Protocol state hash:                           3NKXakPGoujubbXdnPnZrgkcKxtBo2rRNJFs1KyiD7hwExCChmJc
Chain id:                                      5f704cc0c82e0ed70e873f0893d7e06f148524e3f0bdae2afb02e7819a0c24d1
Git SHA-1:                                     c980ba87c3417f40a7081225dfe7478c5ee70fd7
Configuration directory:                       /home/david/.mina-config
Peers:                                         55
User_commands sent:                            0
SNARK worker:                                  None
SNARK work fee:                                100000000
Sync status:                                   Synced
Catchup status:                                
        To build breadcrumb:           0
        To initial validate:           0
        Finished:                      296
        To download:                   0
        Waiting for parent to finish:  0
        To verify:                     0

Block producers running:                       1 (B62qpy6sXLwATHek6wjWKqmDukA7m62rtF1ChoTt1ZMT2po3a4hTW3R)
Coinbase receiver:                             Block producer
```


