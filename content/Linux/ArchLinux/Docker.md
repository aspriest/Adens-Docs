# Docker

## Installation

Installing Docker on Arch Linux is simple, run the command:

```bash
sudo pacman -S docker
```
This downloads the Docker engine which include the the docker daemon to manage containers as well as the Docker CLI.

To activate docker service at boot time run:

```bash
systemctl enable docker.service
```
To start service now:

```bash
systemctl start docker
```

## User Groups

By default only root and users in the docker group can run docker commands. For example I ran into this issue immediatelly when I ran the command:

```bash
docker info
```
 I got the following errror:
>Server:
permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.49/info": dial unix /var/run/docker.sock: connect: permission denied

To avoid this you can either run docker commands with `sudo` or add the current user to the docker group.

Creating docker group and adding user:

```bash
sudo groupadd docker
sudo usermod -aG $USER
```
Intiallt this didn't work and it appeared the user hadn't been added to the docker group. This is because I hadn't restarted the machine. To avoid this I used the following command:

```bash
newgrp docker
```

To sanity check that docker can pull a public image and run a container run:

```bash
docker run hello-world
```