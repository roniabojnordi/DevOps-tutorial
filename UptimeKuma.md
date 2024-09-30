# Uptime Kuma

## To install and run Uptime Kuma using Docker, you can follow the steps below

### Docker installation steps
1. Update Packages: First you need to update your system packages

```
sudo apt update && sudo apt upgrade -y
```

2. Installing Docker: To install Docker, you can use the official Docker repository


```

sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install docker-ce

```
3. Check Docker installation: To ensure successful installation of Docker, you can check its version

```
docker --version
```
4. Install Docker Compose (optional but recommended): If you want to use Docker Compose to manage containers more easily, you can install it

```
sudo curl -L "https://github.com/docker/compose/releases/download/v2.6.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

```
5. To check the version

```
docker-compose --version
```

### Steps to install Uptime Kuma with Docker

#### Installation prerequisites

```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```
#### Add GPG Docker key:

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

#### Add a Docker repository




1. Running Uptime Kuma Container: Docker is a fast and simple way to install Uptime Kuma. You can run Uptime Kuma in a Docker container by running the following command

```
docker run -d --restart=always --name uptime-kuma -p 3001:3001 louislam/uptime-kuma
```
### This command:

-d: Runs the container in background mode.
--restart=always: Ensures that the container runs automatically after a server restart.
--name uptime-kuma: Specifies a name for the container.
-p 3001:3001: port 3001 connects your server to port 3001 inside the container.

2. Accessing Uptime Kuma: After running the container, you can access Uptime Kuma through a browser at the following address

#### Warning

File Systems like NFS (Network File System) are NOT supported. Please map to a local directory or volume.

#### Note

If you want to limit exposure to localhost (without exposing port for other users or to use a reverse proxy), you can expose the port like this

```
docker run -d --restart=always -p 127.0.0.1:3001:3001 -v uptime-kuma:/app/data --name uptime-kuma louislam/uptime-kuma:1
```


‍‍‍
```
http://Ip Server:3001
```

3. Container management

To manage containers, you can use the following commands:

* View the list of containers

```
docker ps
```
* Container stop

```
docker stop uptime-kuma
```

* Restart the container

```
docker start uptime-kuma
```

* View container logs

```
docker logs uptime-kuma
```

* Remove the container
If you need to remove the container

```
docker rm uptime-kuma
```

#### (Optional) Run Uptime Kuma with Docker Compose

If you have Docker Compose installed, you can use the docker-compose.yml file to start Uptime Kuma.

1. System update

```
sudo apt update && sudo apt upgrade -y
```

2. Install Docker and Docker Compose

```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
```
* Check Docker installation
```
docker --version
```

* Install Docker Compose

```
sudo curl -L "https://github.com/docker/compose/releases/download/v2.21.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
* Docker Compose installation review 

```
docker-compose --version
```
3. Create Docker Compose file for Uptime Kuma

* Create a directory for Uptime Kuma

```
mkdir ~/uptime-kuma
cd ~/uptime-kuma
```

To install the latest version of Docker Compose, run the following command

* Create the docker-compose.yml file:
Save the following file in a directory like /opt/uptime-kuma

```
version: '3'
services:
  uptime-kuma:
    image: louislam/uptime-kuma
    container_name: uptime-kuma
    restart: always
    ports:
      - "3001:3001"
    volumes:
      - ./data:/app/data
```

4. Running Kuma Uptime with Docker Compose:

```
docker-compose up -d
```
This command will run the Kuma Uptime container in the background.

5. Access to Uptime Kuma
Now you can access Uptime Kuma through the browser. The address will look like this (according to the server IP)

```
http://[your-server-ip]:3001
```
6. Kuma Uptime Management

* Container stop

To stop the container

```
docker-compose down
```

* Restart the container

To restart the container

```
docker-compose up -d
```
