# Arbitrum Archive Node + Arbitrum Classic Node on Mainnet
 ***HTTP*** request will be available on: ***http://<YOUR_IP>:8547***
 
  ***WS*** request will be available on: ***ws://<YOUR_IP>:8548***
 

 RECOMMENDATION:
 ***configure please your firewall rules (block all income to port 8547,8548,8647,8648 and use whitelist to access to your rpc, more about that can be found:   https://github.com/chaifeng/ufw-docker)***
 
## Hardware Requirements
- At least 8 cores, 16 threads
- 32-GB RAM (64GB of RAM would be perfect)
- 16Tb-NVMe SSD
- Internet Connection: A stable, high-speed internet connection and uninterrupted power supply is crucial!
## Software Requirements
- Docker: The latest versions of Docker and Docker Compose
- Latest Docker Image: offchainlabs/nitro-node:v3.5.0-bdc2fd2 can be found: https://hub.docker.com/r/offchainlabs/nitro-node/tags
- An Ethereum node synced with the mainnet (can be through third-party services)
- Database snapshot: Here’s the link for Arbitrum: https://snapshot.arbitrum.foundation/index.html
- Ethereum L1 and L2 configurations: L1 RPC URL and L2 chain id or name

## Setting Up Arbitrum Database Snapshot:
Let’s start by setting the Arbitrum database snapshot. To access all the snapshots use the link provided before. On the first step of startup, you should utilize the parameter --init.url to initialize the Nitro database. Here’s an example: 

--init.url="https://snapshot.arbitrum.foundation/arb1/nitro-archive.tar"

If you’re setting up multiple nodes, it’s more efficient to download the snapshot image once and host it locally for all your nodes.

For setting more then one Arbitrum node, as well as to run an Arbitrum One Classic node you should use the required parameter: 

--init.url="file:///path/to/snapshot/in/container/snapshot-file.tar due to the presence of classic blocks. However, for running just an Arbitrum One Nitro node this param is optional.

!!! Note that if a database already exists, this setting will be ignored !!!

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
    cd arbitrum-rpc && mkdir .arbitrum && mkdir snapdata && chmod -fR 777 .arbitrum && chmod -fR 777 snapdata
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
    echo 'alias classic_log="docker logs arbitrum-rpc-arb-node-1 -f"' >> $HOME/.profile
    echo 'alias arbitrum_log="docker logs arbitrum-rpc-one-nitro-node-1 -f"' >> $HOME/.profile
    echo 'alias all_log="cd /home/.arbitrum/ && docker compose logs -f"' >> $HOME/.profile
    source $HOME/.profile
    ```
    now you can simply find logs: classic_log, arbitrum_log, and all_log from docker

# You are free to make any changes in docker-compose.yml if you know what you do :wink:

