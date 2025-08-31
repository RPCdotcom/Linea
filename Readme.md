![linea-besu](https://github.com/user-attachments/assets/d5846a7f-11ff-45b6-be16-1b7e5d7872fb)

# Linea Besu Node - RPC Kurulum 

- EN : https://service.rpcdot.com/linea/setup

| Network          | Chain   | ID   |
|--------------------|-------|---------------|
| Mainnet         | Linea | 59144(0xe708)    |


| Node Türü          | RAM   | NVMe Disk Alanı   | İşlemci Çekirdeği | İndirme Hızı |
|--------------------|-------|---------------|-------|-----------|
| Full Node         | +8-16 GB  | +500 GB* | 6+    | +100 mbps  |

| Server Sağlayıcı         | Link              | Features |
|------------------|----------------------------|----------------------------|
| **NetCup**          | [Link](https://www.netcup.com/en/?ref=261820) | Uygun - Vergi %0 |

- Sunucuya Bağlanma : https://github.com/RPCdotcom/Linea/blob/main/Sunucuyanasilbaglanirim.md


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

<img width="815" height="865" alt="image" src="https://github.com/user-attachments/assets/1061ed49-d9a9-426f-b17b-bfa6db2781b9" />


```bash [npx]
VER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep tag_name | cut -d '"' -f 4)
curl -L "https://github.com/docker/compose/releases/download/$VER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
docker-compose --version
```
<img width="993" height="170" alt="image" src="https://github.com/user-attachments/assets/abebe214-c28a-447e-9b04-3280f206a121" />


```bash [npx]
sudo groupadd docker
sudo usermod -aG docker $USER
```

## Linea  Besu İndirelim

```bash [npx]
mkdir linearpc
```

```bash [npx]
cd linearpc
```

```bash [npx]
docker pull consensys/linea-besu-package:latest
```

## Configs ; 
```bash [npx]
wget https://raw.githubusercontent.com/RPCdotcom/Linea/refs/heads/main/docker-compose.yaml
```

<img width="1432" height="59" alt="image" src="https://github.com/user-attachments/assets/9e4a6e5b-4612-48f0-be26-894a659a7443" />


## L1 RPC Değişelim ; 

```bash [npx]
nano docker-compose.yaml
```

<img width="803" height="387" alt="image" src="https://github.com/user-attachments/assets/78b27481-cfd7-4726-bfa1-d94e1f41e7a9" />

- BlockPi'den Aldığımız Ethereum Mainnet RPC ile değiştiriyoruz ; https://dashboard.blockpi.io/rpc/endpoint

<img width="938" height="538" alt="image" src="https://github.com/user-attachments/assets/3375e72a-b0b1-4db6-9b9d-34fe773afd4a" />

- Değiştirdikten sonra CTRL'ye basılı tutup CTRL X ve CTRL Y ardından Enter ile kaydedin.

## Başlatalım ; 
```bash [npx]
docker compose up -d
```

<img width="1419" height="221" alt="image" src="https://github.com/user-attachments/assets/b81d84e4-4c71-46c6-ac32-a75c14c2e86f" />


## Loglar ; 
```bash [npx]
docker logs -f besu-mainnet -n 150
```

- İlk Kurulumda Peer gösterir ve Block İmport yazar ara ara %'delik dilimi gösterip ne kadar sync olduğunu belirtir.

- Tam SYNC Server ; 

<img width="1595" height="639" alt="image" src="https://github.com/user-attachments/assets/3f58bcb4-b2d4-4a85-a31d-50fbbf5c857a" />

#### RPC : 

- Cüzdanınız RPC yada Bağlantı Uç Noktası Kısmında Linea Tarafına Ekleyebilirsiniz : `http://yourserver_ip:8545`

<img width="393" height="590" alt="image" src="https://github.com/user-attachments/assets/aa1ed999-1688-48cc-88fd-2721ecdba84d" />
