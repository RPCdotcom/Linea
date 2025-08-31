![linea-besu](https://github.com/user-attachments/assets/d5846a7f-11ff-45b6-be16-1b7e5d7872fb)

# Linea Besu Node - RPC Kurulum 

- EN : https://service.rpcdot.com/linea/setup

| Network          | Chain   | ID   |
|--------------------|-------|---------------|
| Mainnet         | Linea | 59144(0xe708)    |


| Node Türü          | RAM   | NVMe Disk Alanı   | İşlemci Çekirdeği | İndirme Hızı |
|--------------------|-------|---------------|-------|-----------|
| Full Node         | +8-16 GB  | +500 GB* | 6+    | +100 mbps  |


## Güncelleme - Foşur Foşur Temizleme + Yenileme

```bash [npx]
sudo apt update && sudo apt upgrade -y
sudo apt install htop ca-certificates zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev tmux iptables curl nvme-cli git wget make jq libleveldb-dev build-essential pkg-config ncdu tar clang bsdmainutils lsb-release libssl-dev libreadline-dev libffi-dev jq gcc screen file nano btop unzip lz4 -y
```

## Docker İndirelim Sıra Sıra Girin

```bash [npx]
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io -y
docker version
```

```bash [npx]
VER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep tag_name | cut -d '"' -f 4)
curl -L "https://github.com/docker/compose/releases/download/$VER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
docker-compose --version
```


```bash [npx]
sudo groupadd docker
sudo usermod -aG docker $USER
```

## Linea Hyperledger Besu İndirelim

```bash [npx]
wget https://docs.linea.build/files/besu/besu-mainnet.zip
unzip besu-mainnet.zip
```

- Besu Dosyasına Girelim ; 

```bash [npx]
cd besu-mainnet
```

## Configs ; 
```bash [npx]
curl -Ls https://raw.githubusercontent.com/RPCdotcom/Linea/refs/heads/main/docker-compose.yaml > $HOME/besu-mainnet/docker-compose.yaml
```

## Başlatalım ; 
```bash [npx]
docker compose up -d
```

## Loglar ; 
```bash [npx]
docker logs -f besu-mainnet -n 150
```

#### RPC : 

- Cüzdanınız RPC yada Bağlantı Uç Noktası Kısmında Linea Tarafına Ekleyebilirsiniz : `http://yourserver_ip:8549`
