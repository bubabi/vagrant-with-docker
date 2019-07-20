# docker-with-vagrant

<img src="https://technology.amis.nl/wp-content/uploads/2015/08/image70.png" alt="cover" width="355px" height="280px">


This repository purposes to create a Vagrant box and to enable the Docker Daemon used from _2375_ port with the Docker Host parameter (-H). This allows you can easily use the Docker Daemon from a remote Docker Client.

## Usage

Perform the following commands in the folder where the Vagrantfile file is located.

**Run the VM**
```shell
vagrant up
vagrant ssh
```

**Client Machine**

```shell
docker -H tcp://<BOX_IP>:2375 <DOCKER_COMMAND>
```

## Packaging the Box

If you want to package the virtual machine you have configured with Vagrant for later use or to share it with others: 

**--base**: shows the virtual machine on which we will base, in this case VM name "_build\_box_"

**--vagrantfile**: the Vagrantfile containing the custom configurations we want when the packaged machine starts up again

Run this command where the Vagrantfile.pkg file is located, as well as when your base virtual machine is running.

```shell
vagrant package --base build_box --vagrantfile Vagrantfile.pkg
```

After this command, the packaged box file, **_package.box_**, was created. 

Then you can run this box at any time by following the steps below,

```shell
vagrant box add package.box pkg_box
vagrant init pkg_box
vagrant up
```

The box is now ready to use, you can connect with SSH.

**OS used in the box**: alpine linux 2.6.0

**Packaged box size**: ~88MB

##### [cover source](https://technology.amis.nl/2015/08/22/first-steps-with-provisioning-of-docker-containers-using-vagrant-as-provider/)

