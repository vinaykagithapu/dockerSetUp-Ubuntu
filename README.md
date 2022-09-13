# dockerSetUp-Ubuntu
This will guide you to setup docker in Ubuntu operating system.

# Getting Started
## Setup
1. Uninstall old versions
```shell
sudo apt-get remove docker docker-engine docker.io containerd runc -y
```
2. Update the apt package index and install packages to allow apt to use a repository over HTTPS
```shell
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg lsb-release -y
```
3. Add Docker’s official GPG key
```shell
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
4. Use the following command to set up the repository
```shell
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
5. Update the apt package index, and install the latest version of Docker Engine, containerd, and Docker Compose, or go to the next step to install a specific version
```shell
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
```

## Verify
1. Verify that Docker Engine is installed correctly by running the hello-world image
```shell
sudo service docker start
sudo docker run hello-world
```

## Manage Docker as a non-root user
1. Create the docker group
```shell
sudo groupadd docker
```
2. Add your user to the docker group
```shell
sudo usermod -aG docker $USER
```
3. Log out and log back in so that your group membership is re-evaluated
4. Verify that you can run docker commands without sudo
```shell
docker run hello-world
```

# CleanUp
1. Uninstall the Docker Engine, CLI, Containerd, and Docker Compose packages
```shell
sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
```
2. Images, containers, volumes, or customized configuration files on your host are not automatically removed. To delete all images, containers, and volumes
```shell
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```