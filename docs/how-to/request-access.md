
# How to request access to the platform

To get access to the platform you need to perform these operations:

* Request access to the VPN
* Request access to the cluster

## Request access to the VPN

### - `unibo` credential users

If you are owner of a `unibo` credential you can directly request access to the VPN by sending an email to `ciro.barbone@unibo.it`. 
When you will be granted access you will receive an email with the instructions to connect to the VPN.

### - `studio.unibo` credential users

If you have a `studio.unibo` account, you must contact your supervisor that will request access to the VPN for you. 
When you will be granted access you will receive an email with the instructions to connect to the VPN.

You'll not be able to directly access the Portainer Dashboard with your credential, your supervisor will provide you with a container on which you'll be able to access through its web service (or ssh service, depending on the container configuration).
  
## Request access to the cluster

After you are granted to use the VPN, you can access the Portainer dashboard at [https://andromeda.apice.unibo.it:8006](https://andromeda.apice.unibo.it:8006), however, you will not be able to login.

Your supervisor will ask the cluster administrators to give you access to the cluster, and after that, you will be able to login to the Portainer dashboard with your institutional credentials (the same used for the VPN). 
When logging in, select the correct authentication realm from the list, for instance, if you have a `unibo` credential, select the `unibo` realm, if you have a `studio.unibo` credential, select the `studio.unibo` realm.

![](./images/proxmox_login.png)


## Request a MAC address
To deploy a container, you need to provide a unique MAC address for it. You can ask your supervisor to assign you a valid MAC address. 

Your supervisor can use this website to assign you a MAC address: [https://padfy.campusfc.unibo.it/](https://padfy.campusfc.unibo.it/).


