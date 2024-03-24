# Arbitrum rpc node on mainnet
 ***HTTP*** request will be available on: ***http://<YOUR_IP>:8647***
 
  ***WS*** request will be available on: ***ws://<YOUR_IP>:8648***
 

 RECOMMENDATION:
 ***configure please your firewall rules (block all income to port 8547,8548,8647,8648 and use whitelist to access to your rpc, more about that can be found:   https://github.com/chaifeng/ufw-docker)***
 
## Following parameters:
- 16-CPU
- 32-GBRAM
- 16Tb-NVMe SSD

## First Step
- **Update packages**
    ```
    sudo apt update && sudo apt upgrade -y
    ```
- **Install dependencies**
     ```
     sudo apt install curl build-essential git wget jq make gcc nano htop tmux -y
     ```
- **Install docker and docker compose**
    ```
    curl -fsSL https://get.docker.com -o get-docker.sh
    sudo sh ./get-docker.sh
    docker version && docker compose version
    ```

- **Run Docker as a non-root user**
    ```
    sudo usermod -aG docker <your_user>
    ```

### Relogin to your server to take effect from usermod !!!

## Second Step 
- **Clone this repo to your server, navigate to arbitrum-rpc folder and spin up all docker containers**
    ```
    git clone https://github.com/andrii1890/arbitrum-rpc.git
    cd arbitrum-rpc
    ```
  **!!!Cange your L1 eth provider in docker-compose.yml**

    ```
    nano docker-compose.yml
    ```
    ```
    docker compose up -d
    ```

## Third step
- **Add alias for docker logs**
    ```
    echo "#Arbitrum Node Logs" >> $HOME/.profile
    echo 'alias classic_log="docker logs arbitrum-arb-node-1 -f"' >> $HOME/.profile
    echo 'alias arbitrum_log="docker logs goerli-rpc-lighthouse-1 -f"' >> $HOME/.profile
    echo 'alias all_log="cd /home/.arbitrum/ && docker compose logs -f"' >> $HOME/.profile
    source $HOME/.profile
    ```
    now you can simply find logs: classic_log, arbitrum_log, and all_log from docker

# You are free to make any changes in docker-compose.yml if you know what you do :wink:

