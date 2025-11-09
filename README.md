# codeassit-guide-for-VPS-users
## Hardware Requirements 
- **RAM**: 12GB+  
- **Disk**: 10GB+ SSD
  
> 💡 Tip: You can check [servarica.com](https://servarica.com) for affordable servers.

## 1. Prerequisites  

### Update packages
```bash
sudo apt-get update && sudo apt-get upgrade -y
```

### Install dependencies
```bash
sudo apt install curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip ufw screen gawk -y
```

### Install Docker
```bash
sudo apt update -y && sudo apt upgrade -y
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg -y
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y && sudo apt upgrade -y
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y

# Test Docker
sudo docker run hello-world

sudo systemctl enable docker
sudo systemctl restart docker
```

---

## 2. Install UV
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

## 3. Clone the repo and Go into directory
```bash
git clone https://github.com/gensyn-ai/codeassist.git
```
```bash
cd codeassist
```

### now to start the node, you'll need huggingface token with write permission
- **Go to `https://huggingface.co/` and create account if you currently don't have one**
- **Click profile photo by top right, click access tokens**
  <img width="1440" height="779" alt="image" src="https://github.com/user-attachments/assets/8bdc20d0-de95-41ab-96d3-07a1e2c8bfa4" />
- Now click create new token, select write, input any name and create
<img width="1009" height="469" alt="image" src="https://github.com/user-attachments/assets/098b1991-a682-4a79-b3ed-50e130a844dd" />
- copy the token and save it somewhere

## 4. Enter this command in your directory to run codeassist 
```bash
uv run run.py
```
**it,ll ask for your huggingface token, enter the access token you created and let it build**
**takes a couple of minutes to set up the containers so be patient**

**Once it gets here and asks you to open url on browser, you'll need to forward ports over SSH**
