# Good Practices

Cluster resources are shared among all users, so it is important to follow some good practices to avoid conflicts with them. 

1. Each container should be run with a unique name, following the pattern: `<name>.<surname>-<purpose>`.
2. Each container could possibly reserve all the resources of a node of the cluster, so it is important to specify only the amount of resources that are really needed to run the experiments.
3. Each container allocation is temporary, this means that if not needed anymore it **must** be stopped and removed. This is important to avoid wasting resources and to allow other users to run their experiments.

# Persistency

By default, all the data generated inside a container is lost when the container is stopped and removed (or restarted). 
To avoid this, the shared storage must be correctly used upon container configuration.
When creating a container, in the `Disks` tab, you must select the `shared-storage-antares` shared storage, otherwise and you will not be able to save your work in a persistent way.