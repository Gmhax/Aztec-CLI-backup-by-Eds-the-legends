# Aztec-CLI-backup-by-Eds-the-legends


1. Remove the Aztec installation directory
```
rm -rf ~/.aztec
```
```
sed -i '/export PATH="\$HOME\/\.aztec\/bin:\$PATH"/d' ~/.bashrc
```

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
4. Create session
```
screen -S aztec
```
5. Execute:
```
aztec start --node --archiver --sequencer \
  --network alpha-testnet \
  --l1-rpc-urls RPC_URL  \
  --l1-consensus-host-urls BEACON_URL \
  --sequencer.validatorPrivateKeys 0xYourPrivateKey \
  --sequencer.coinbase 0xYourAddress \
  --p2p.p2pIp IP
```

# Done Eds



