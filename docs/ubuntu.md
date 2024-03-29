
## Install Ubuntu

### Disk Partition

- EFI: 500mb
- SWAP: 8192mb
- EXT4 Boot: 100mb
- EXT: all remain

### After Installation

Update ubuntu

```bash
sudo apt-get update && sudo apt-get upgrade
```

```bash
sudo apt install curl vim tree wget git htop tmux
sudo apt install imagemagick ffmpeg 
```

### Configure Git

```bash
git config --global user.name "Mert Cobanov"
git config --global user.email "<mertcobanov@gmail.com>"
git config --global init.defaultBranch 'main'
git config --global credential.helper store
```

## Install Zsh

Read this
<https://gist.github.com/n1snt/454b879b8f0b7995740ae04c5fb5b7df>

### Make default

```bash
sudo nano ~/.bashrc
exec zsh
```
## Docker

```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
apt-cache policy docker-ce
sudo apt install docker-ce -y
sudo systemctl status docker 
sudo su
useradd -m -s /bin/bash docker -g docker
su docker
docker run hello-world
```

## Portainer

```bash
docker volume create portainer_data
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

## Create User

```
sudo adduser fethi
sudo usermod -aG sudo fethi

sudo chown fethi:fethi /developer
sudo chmod u+rw /developer
```
## GPU Drivers

```bash
sudo apt update & upgrade
sudo apt install nvidia-driver-525 # Check the latest
nvidia-smi
```

```bash
lspci | grep -i nvidia
sudo apt install build-essential
gcc --version
g++ --version
sudo apt install nvidia-cuda-toolkit
nvcc --version
```

## Install Miniconda

```bash
curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
```

### Torch environment

```bash
conda create --name torchenv python=3.9
activate torchenv

conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia
```

```python
import torch
torch.cuda.is_available()
```

## Docker with NVIDIA Container Runtime

```bash
sudo apt-get update
```

```bash
sudo apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

```bash
sudo apt update
apt-cache policy docker-ce
```

```bash
sudo apt install docker-ce
sudo systemctl status docker

sudo docker run hello-world
```

## NVIDIA Container Runtime

```bash
curl -s -L https://nvidia.github.io/nvidia-container-runtime/gpgkey | \
  sudo apt-key add -
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-container-runtime/$distribution/nvidia-container-runtime.list | \
  sudo tee /etc/apt/sources.list.d/nvidia-container-runtime.list
sudo apt-get update
```

```bash
sudo apt-get install nvidia-container-runtime
```

```bash
docker run --gpus all nvidia/cuda:12.1.0-base-ubuntu22.04 nvidia-smi
```
