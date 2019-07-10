# docker-with-vagrant

This repository purposes to create a Vagrant box and to enable the Docker Engine used from _2375_ port with the Docker Host. This allows you can use easily the Docker Engine from a remote Docker Client.

## Usage

**Run the VM**
```shell
vagrant up
vagrant ssh
```

**Client Machine**

```shell
docker -H tcp://<BOX_IP>:2375 <DOCKER_COMMAND>
```
