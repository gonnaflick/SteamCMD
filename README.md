# SteamCMD Installation
* [General info](#general-info)
* [Instructions](#instructions)
* [Sources](#sources)
## General info
This is an automated build for SteamCMD implemented in Docker. It can be used as a base image for any game server. The image is implemented in Ubuntu and only contains the necessary dependencies for a server to work. This image was created to be used with the `Rust Game Server image` but can also be used with other type of servers if needed.

## Instructions
There are two types of implementation.

### FROM docker implementation
The ideal or intended way for the image to work is by using it as a base image for other container, essentially it provides you with an Ubuntu build with everything you need to implement your SteamCMD servers.
1. Just include the following text in your Dockerfile. Implementation as root
```
FROM gonnaflick/steamcmd:root
```
Implementation as user:
```
FROM gonnaflick/steamcmd:user
```
The Docker images are found in the following repository: https://hub.docker.com/repository/docker/gonnaflick/steamcmd

### Building the container implementation
1. Clone the repository 

```
$ git clone https://github.com/gonnaflick/SteamCMD.git
```
2. Enter to the directory for the type of user you preffer to work on the container, either user or root.
```
$ cd SteamCMD/root
```
Or
``` 
$ cd SteamCMD/user
```
3. Build the image
```
$ docker build -t steamcmd-image .
```
4. Find the Docker image ID from the tag `steamcmd-image`. You can find it with the following command
```
$ docker images
```
5. Run the docker image and create the container. Here is a command example:
```
$ docker run -it --name <CONTAINER-NAME> <IMAGE-ID> /bin/bash
```

## Sources
* https://hub.docker.com/repository/docker/gonnaflick/steamcmd
* https://developer.valvesoftware.com/wiki/SteamCMD#Linux
* https://github.com/CM2Walki
