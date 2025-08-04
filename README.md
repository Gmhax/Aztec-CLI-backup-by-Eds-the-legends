# Aztec attestation 

## Still seeing “missed” on attestation? Chill, bro — I got you.
<img width="902" height="436" alt="image" src="https://github.com/user-attachments/assets/7215f16f-ca0a-4b84-8ca1-ab94da40b746" />


- Stop the node:
```
# Stop docker containers
docker stop $(docker ps -q --filter "ancestor=aztecprotocol/aztec") && docker rm $(docker ps -a -q --filter "ancestor=aztecprotocol/aztec")

# Stop screens
screen -ls | grep -i aztec | awk '{print $1}' | xargs -I {} screen -X -S {} quit
```
- Delete old data
```
bash <(curl -Ls https://raw.githubusercontent.com/DeepPatel2412/Aztec-Tools/refs/heads/main/Aztec%20CLI%20Cleanup)
```

1. Remove the Aztec installation directory
```
sudo find / -type f -iname '*aztec*' -exec rm -f {} \;
```
```
sudo find / -type d -iname '*aztec*' -exec rm -rf {} \;
```
```
docker ps -a --format "{{.ID}} {{.Image}}" | grep aztec | awk '{print $1}' | xargs -r docker rm -f
```
```
docker images --format "{{.Repository}} {{.ID}}" | grep aztec | awk '{print $2}' | xargs -r docker rmi -f
```
```
docker volume ls --format "{{.Name}}" | grep aztec | xargs -r docker volume rm
```
```
rm -rf ~/aztec*
rm -rf ~/aztec-node*
rm -rf ~/.aztec*
```
- To confirm if everything is gone:
```
sudo find / -iname '*aztec*'
```
- If no result appears, ✔️ Aztec is completely removed from your system.

2. Install Aztec Tools
```
bash -i <(curl -s https://install.aztec.network)
```
```
echo 'export PATH="$HOME/.aztec/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```
```
aztec
```
3. Update Aztec
```
aztec-up latest
aztec-up 1.2.0
```
4. Enable the firewall and open the required ports (if you’ve already done this before, you can ignore this step).
```
# Firewall
ufw allow 22
ufw allow ssh
ufw enable

# Sequencer
ufw allow 40400
ufw allow 8080
```
- Create aztec directory:
```
mkdir aztec
cd aztec
```
5. Create .env
```
nano .env
```
- Replace the following code in .env
```
ETHEREUM_RPC_URL=RPC_URL
CONSENSUS_BEACON_URL=BEACON_URL
VALIDATOR_PRIVATE_KEYS=0xPrivatekey1
COINBASE=0xYourAddress
P2P_IP=P2P_IP
```

6. Create docker-compose.yml:
```
nano docker-compose.yml
```
- Replace the following code in docker-compose.yml
```
services:
  aztec-node:
    container_name: aztec-sequencer
    image: aztecprotocol/aztec:1.2.0
    restart: unless-stopped
    environment:
      ETHEREUM_HOSTS: ${ETHEREUM_RPC_URL}
      L1_CONSENSUS_HOST_URLS: ${CONSENSUS_BEACON_URL}
      DATA_DIRECTORY: /data
      VALIDATOR_PRIVATE_KEYS: ${VALIDATOR_PRIVATE_KEYS}
      COINBASE: ${COINBASE}
      P2P_IP: ${P2P_IP}
      LOG_LEVEL: info
    entrypoint: >
      sh -c 'node --no-warnings /usr/src/yarn-project/aztec/dest/bin/index.js start --network alpha-testnet --node --archiver --sequencer'
    ports:
      - 40400:40400/tcp
      - 40400:40400/udp
      - 8080:8080
    volumes:
      - /root/.aztec/alpha-testnet/data/:/data
```
- You dont need to change anything. 
- Run Node Docker:
```
docker compose up -d
```
- Node Logs:
```
docker compose logs -fn 1000
```



# Done Ma-bro..



































