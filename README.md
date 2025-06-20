
```
sudo apt-get update && sudo apt-get upgrade -y
sudo apt install curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev screen ufw -y
```

```
sudo ufw allow 22
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw allow ssh
sudo ufw enable
sudo ufw reload
```
```
sudo bash -c 'cat > /etc/sysctl.d/99-popcache.conf << EOL
net.ipv4.ip_local_port_range = 1024 65535
net.core.somaxconn = 65535
net.ipv4.tcp_low_latency = 1
net.ipv4.tcp_fastopen = 3
net.ipv4.tcp_slow_start_after_idle = 0
net.ipv4.tcp_window_scaling = 1
net.ipv4.tcp_wmem = 4096 65536 16777216
net.ipv4.tcp_rmem = 4096 87380 16777216
net.core.wmem_max = 16777216
net.core.rmem_max = 16777216
EOL'
sudo sysctl -p /etc/sysctl.d/99-popcache.conf
```

```
sudo bash -c 'cat > /etc/security/limits.d/popcache.conf << EOL
*    hard nofile 65535
*    soft nofile 65535
EOL'
```

```
sudo mkdir -p /opt/popcache
sudo mkdir -p /opt/popcache/logs
wget https://github.com/traderaman/pipe2/raw/refs/heads/main/pop-v0.3.2-linux-x64.tar.gz
sudo mv ~/pop-v0.3.2-linux-x64.tar.gz /opt/popcache/
cd /opt/popcache/
```
```
sudo tar -xzf pop-v0.3.2-linux-x64.tar.gz
sudo chmod +x ./pop
chmod 777 pop-v0.3.2-linux-x64.tar.gz
sudo ln -sf /opt/popcache/pop /usr/local/bin/pop
sudo nano config.json
```

```
{
  "pop_name": "your-pop-name",
  "pop_location": "Your Location, Country",
  "invite_code": "Enter your Invite Code",
  "server": {
    "host": "0.0.0.0",
    "port": 443,
    "http_port": 80,
    "workers": 0
  },
  "cache_config": {
    "memory_cache_size_mb": 4096,
    "disk_cache_path": "./cache",
    "disk_cache_size_gb": 100,
    "default_ttl_seconds": 86400,
    "respect_origin_headers": true,
    "max_cacheable_size_mb": 1024
  },
  "api_endpoints": {
    "base_url": "https://dataplane.pipenetwork.com"
  },
  "identity_config": {
    "node_name": "your-node-name",
    "name": "Your Name",
    "email": "your.email@example.com",
    "website": "https://your-website.com",
    "discord": "your_discord_username",
    "telegram": "your_telegram_handle",
    "solana_pubkey": "YOUR_SOLANA_WALLET_ADDRESS_FOR_REWARDS"
  }
}
```

```
sudo bash -c 'cat > /etc/systemd/system/popcache.service << EOL
[Unit]
Description=POP Cache Node
After=network.target

[Service]
Type=simple
User=root
Group=root
WorkingDirectory=/opt/popcache
ExecStart=/opt/popcache/pop
Restart=always
RestartSec=5
LimitNOFILE=65535
StandardOutput=append:/opt/popcache/logs/stdout.log
StandardError=append:/opt/popcache/logs/stderr.log
Environment=POP_CONFIG_PATH=/opt/popcache/config.json

[Install]
WantedBy=multi-user.target
EOL'
```

```
sudo systemctl daemon-reload
sudo systemctl enable popcache
sudo systemctl start popcache
sudo apt install bc
source <(curl -s https://raw.githubusercontent.com/astrostake/0G-Labs-script/refs/heads/main/storage-node/check_block.sh)
```


![image](https://github.com/user-attachments/assets/46e9cac6-66e8-4e37-83e1-f7dce5e9bb2f)


# Stop the service 

```
sudo systemctl stop popcache
```

# Next day command for local pc

```
sudo systemctl restart popcache
```




<div align="center">

# 📈 Upgrade to new release/version (v0.3.2) {Local/Vps} 

![image](https://github.com/user-attachments/assets/0cec40ba-dbe3-4f53-92f8-f99b6104cc66)



</div


* Stop popcache service

```
sudo systemctl stop popcache
```

* Delete old binary 

```
sudo rm -f /usr/local/bin/pop

```
```
sudo rm -f /opt/popcache/pop
```

```
sudo rm -f /opt/popcache/pop-v0.3.0-linux-x64.tar.gz && sudo rm -f /opt/popcache/pop-v0.3.1-linux-x64.tar.gz
```

* Delete old logs data

```
sudo rm /opt/popcache/logs/stderr.log
```

```
sudo rm /opt/popcache/logs/stdout.log
```

* Now follow the [Download the binary](https://github.com/Mayankgg01/Pipe-Testnet-Node-Guide?tab=readme-ov-file#download-the-binary) process:

* After that Reload & Start the service:

```
sudo systemctl daemon-reload
```

```
sudo systemctl start popcache
```

* You dont need to do [Set Configuration File](https://github.com/Mayankgg01/Pipe-Testnet-Node-Guide?tab=readme-ov-file#set-configuration-file) process now:
 
* You can check the Logs and file status:

* If logs return `⚠️  Mesh test service temporarily unavailable` ,  then Just restart Your service with: 

```
sudo systemctl restart popcache
```
* If still the same log then just wait for few hours or days than restart:

![image](https://github.com/user-attachments/assets/9fc6e18a-db3a-4fea-811f-efaad545b16f)




<div align="center">

# 🏃 Path where u need to move `pop-v0.3.2-linux-x64.tar.gz` for LOCAL PC 🏃


</div


**------For the people who are facing issue while running pipe on local pc-- they are confused that where we have to move or drop the `pop-v0.3.2-linux-x64.tar.gz` file: So u have to watch this video for understing much batter:**

* **Process**: 

👉 Goto This Pc>Linux🐧>Ubuntu>Home>Your_wls_username>Paste_your_`pop-v0.3.2-linux-x64.tar.gz`_file

**Video Refrence-** 👇


https://github.com/user-attachments/assets/2a932bfc-df13-4c73-816a-f0297f244b92



* After paste the `pop-v0.3.2-linux-x64.tar.gz` file to your wsl path, **follow the process to unzip & move**:

 
```
sudo mv ~/pop-v0.3.2-linux-x64.tar.gz /opt/popcache/
```

```
cd /opt/popcache/
```

```
sudo tar -xzf pop-v0.3.2-linux-x64.tar.gz
sudo chmod +x ./pop
chmod 777 pop-v0.3.2-linux-x64.tar.gz
sudo ln -sf /opt/popcache/pop /usr/local/bin/pop
```

* **After that follow all steps from** [Set Configuration File](https://github.com/Mayankgg01/Pipe-Testnet-Node-Guide?tab=readme-ov-file#set-configuration-file)



If U have any issue then open a issue on this repo or Dm me on TG~


👉 Join TG for more Updates: https://telegram.me/cryptogg

Thank U! 👾

Happy Coding💗


