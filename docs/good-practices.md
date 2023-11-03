# Good Practices

Users can deploy their own experiments in the cluster on which they are granted to work. 
Cluster resources are shared among all users, so it is important to follow some good practices to avoid conflicts with them. 

1. Each container should be run with a unique name, following the pattern: `<name>.<surname>-<purpose>`.
2. Each container could possibly reserve all the resources of a node of the cluster, so it is important to specify only the amount of resources that are really needed to run the experiments.
3. Each container allocation is temporary, this means that if not needed at a certain moment, it **must** be stopped and removed. This is important to avoid wasting resources and to allow other users to run their experiments.
4. Each Sunday at 1:30 AM cluster machines are configured to perform automatic updates, sometimes this operation requires the reboot of the machine. To avoid the loss of data, it is important to save the data on a persistent volume.

# Persistency

By default, all the data generated inside a container is lost when the container is stopped and removed (or restarted). 
To avoid this, it is possible to configure the container to use a Docker persistent volume. 
Basically, a persistent volume is a directory on the host machine that could be mounted into a container. 
Each cluster's user is granted to use a persistent volume, provided by the cluster administrators.

To use a persistent volume when running a container, the user must specify the volume name and the mount path inside of the container. 

!!! seealso
    See [Docker Volumes](./explanation/docker-swarm.md#volumes) for more information about Docker volumes.
