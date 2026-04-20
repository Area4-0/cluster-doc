# How to access deployed container

You can access your container through the network, using the hostname you provided during the container creation.
For instance, if you provided `m.baiardi-experiment-network` as hostname, you can access the container using `ssh m.baiardi-experiment-network` if you configured the SSH server inside of the container and you provided a SSH public key during the container creation.