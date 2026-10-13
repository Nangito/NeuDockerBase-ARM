# NeuDockerbase futtatása ARM alapú processzorokon!

# A következő pár lépés akkor szükséges ha az előre elkészített image nem áll rendelkezésre
- A virtuális gép felépítéséhez szükséges az Ubuntu ARM szerver image, ami a következő linkről letölthető: [Ubuntu](https://ubuntu.com/download/server/arm)
- Automatikus telepítés során adjunk neki Felhasználónevet és Jelszavat
- Adjunk neki 4 processzor magot és 4GB ramot
- A következő portokat forwardoljuk: 


| Name | Protocol | Host IP | Host Port | Guest IP | Guest Port |
| :--- | :--- | :--- | :--- | :--- | :--- |
| HTTP | TCP | 127.0.0.1 | 80 | | 80 |
| HTTP2 | TCP | 127.0.0.1 | 8080 | | 8080 |
| JSON_Server | TCP | 127.0.0.1 | 8888 | | 8888 |
| MSSQL | TCP | 127.0.0.1 | 1433 | | 1433 |
| MySQL | TCP | 127.0.0.1 | 3306 | | 3306 |
| Node | TCP | 127.0.0.1 | 3000 | | 3000 |
| PostgreSQL | TCP | 127.0.0.1 | 5432 | | 5432 |
| SSH | TCP | 127.0.0.1 | 22 | | 22 |
| Vite | TCP | 127.0.0.1 | 5173 | | 5173 |

***


# Az image indítása előtt szükség lesz a következőkre(Szükséges lépés meglévő imaggel is):

```
sudo nano /etc/hosts
```
## Másoljuk a következőt bele:
```
127.0.0.1       vm1.test api.vm1.test frontend.vm1.test responsive.vm1.test backend.vm1.test pma.vm1.test docs.vm1.test$
```
***
```
sudo nano ~/.ssh/config
```
## Másoljuk a következőt bele:
*Note: A 22-es port alapártelmezetten foglalt Mac-en*
```
Host vm1.test
	HostName vm1.test 
	Port 10022
```
***


# A Linux imagen belül:

```
sudo apt-get update && sudo apt-get upgrade -y
```
```
sudo apt install -y \
  ansible \
  apache2 \
  bash \
  bash-completion \
  bsdutils \
  build-essential \
  ca-certificates \
  certbot \
  curl \
  dash \
  diffutils \
  dkms \
  docker.io \
  docker-compose-v2 \
  fail2ban \
  findutils \
  just \
  git \
  grep \
  gzip \
  hostname \
  htop \
  init \
  jq \
  login \
  make \
  man-db \
  manpages \
  mariadb-server \
  mc \
  ncdu \
  ncurses-base \
  ncurses-bin \
  net-tools \
  nginx \
  nodejs \
  npm \
  openssh-server \
  p7zip-full \
  perl \
  php-cli \
  php-fpm \
  php-mysql \
  postgresql \
  postgresql-contrib \
  python3 \
  python3-certbot-nginx \
  python3-pip \
  python3-venv \
  tree \
  ubuntu-minimal \
  ubuntu-server \
  ubuntu-server-minimal \
  ubuntu-standard \
  ufw \
  unzip \
  util-linux \
  wget \
  zip && \
sudo npm install -g pm2
```

# A [FullStack](https://github.com/rcsnjszg/fullstack2627.git) alapon belül:
```
sudo apt remove just
```
```
mkdir -p ~/bin
```
```
curl --proto '=https' --tlsv1.2 -sSf https://just.systems/install.sh | bash -s -- --to ~/bin
```
```
export PATH="$PATH:$HOME/bin"
```

*Ellenőrzés (Legfrissebb verzónak kell lennie)*
```
just --version
```

***

# NOTE: Docker imagek-et ez nem tartalmaz!

*Docker Permission error fix:*
```
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
```
## Ellenőrzés:

```
groups
```

