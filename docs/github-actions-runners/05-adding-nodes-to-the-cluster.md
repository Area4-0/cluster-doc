# Adding nodes to the k3s cluster

Now that you have a running k3s cluster and ARC correctly installed, you can start expanding your cluster by adding new nodes according to your resource needs.
There are two ways to add a new node to the cluster: manually, or using Infrastructure as Code (Terraform + Ansible) for a more automated approach.

## Retrieving the join token

In both cases you will need to retrieve the join token from the master.
This token will be used during the installation of k3s on the new machine.

Execute this command on your master:

```bash
sudo cat /var/lib/rancher/k3s/server/node-token
```

Copy the output and store it securely, since it is sensitive information.

## How to add a node: manual setup

Create a virtual machine using the Proxmox UI. For a guide on how to create a virtual machine or an LXC container, check
[how to deploy a container](../how-to/deploy-container.md).

Install `curl`, if it is not already installed.

```bash
sudo apt update && sudo apt install curl -y
```

Install k3s, completing the command with the IP address of your master and the token previously retrieved.

```bash
curl -sfL https://get.k3s.io | K3S_URL=https://...:6443 K3S_TOKEN=... sh -
```

Now, to verify that everything worked correctly, execute this command on the master:

```bash
kubectl get nodes
```

You should be able to see the new node.

## How to add a node: Terraform + Ansible setup

### Prerequisites

- Terraform installed on your machine. Check the
  [official documentation](https://developer.hashicorp.com/terraform/install).
- Ansible installed on your machine. Check the
  [official documentation](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).
- Access credentials to your Proxmox instance (API token or user/password).

### How to get your Proxmox API token

Log in to the Proxmox web UI, go to `Datacenter` > `Permissions` > `API Tokens` and click `Add`.
Now select the user the token will belong to and enter a `Token ID`, a name to identify the token's purpose.
Lastly, click `Add`.

!!! warning
    The token secret is shown only once, right after creation. Copy it
    immediately and store it securely.

### Provisioning the virtual machine with Terraform

The Terraform scripts in [this repository](https://github.com/Thesis-repositories/K3s-new-node) provision a new VM on Proxmox by cloning it from an existing template, using the `bpg/proxmox` provider.

Clone the repository and move into the `Terraform` folder:

```bash
git clone https://github.com/Thesis-repositories/K3s-new-node.git
cd K3s-new-node/Terraform
```

Create a `terraform.tfvars` file in this folder with your actual values, you can check the file `variables.tf` for a better understanding of what these variables should contain:

```hcl
proxmox_api_url = "https://andromeda.apice.unibo.it:8006/"
proxmox_api_token = "<USER>!<TOKEN_ID>=<TOKEN_SECRET>"
vm_mac_address = "<VM_MAC_ADDRESS>"
ssh_public_key = "<YOUR_PUBLIC_KEY>"
vm_hostname = "<VM_HOSTNAME>"
target_node = "<A_PROXMOX_CLUSTER_NODE>"
template_node = "iris"
template_id = 100
```

!!! note
    The MAC address of the new machine has to be a valid address and needs to be assigned by a supervisor (In the next section you will also need the corresponding IP address). 

!!! note
    There is already a cloud-init template inside the cluster. It is in the node "iris", and its VM ID is 100.

!!! note
    `vm_cpu_cores` (default 2) and `vm_memory` (default 2048 MB) are optional and can be omitted from `terraform.tfvars` if the defaults are fine for your setup.

!!! warning
    `terraform.tfvars` contains sensitive values (the Proxmox API token) and is already excluded via `.gitignore`.

Initialize Terraform with:

```bash
terraform init
```

Now you can apply the configuration:

```bash
terraform apply
```

Terraform will show the planned changes and ask for confirmation before creating the VM.

!!! note
    Even after the `Apply complete!` message, you probably won't be able to access the new virtual machine yet, and will get a `Connection refused` error when trying to connect via SSH. This happens because the machine is still initializing, wait a couple of minutes and try again.

### Configuring k3s with Ansible

Once the VM is up and running, the
[Ansible playbook](https://github.com/Thesis-repositories/K3s-new-node/blob/main/Ansible/join-k3s.yaml) installs k3s in agent mode and joins it to the existing cluster.

Move into the `Ansible` folder:

```bash
cd ../Ansible
```

Create an `inventory.ini` file listing the new node:

```bash
[new_nodes]
vm1 ansible_host=<IP_ADDRESS_OF_THE_NEW_MACHINE> ansible_user=ubuntu ansible_ssh_private_key_file=<PATH_TO_YOUR_PRIVATE_KEY> ansible_ssh_common_args='-o StrictHostKeyChecking=no'
```

!!! note
    `ansible_user` must be `ubuntu`, since that's the user configured via cloud-init in the Terraform step.

!!! note
    `ansible_ssh_private_key_file` must point to the private key matching the public key passed as `ssh_public_key` in `terraform.tfvars`.

!!! note
    `ansible_ssh_common_args='-o StrictHostKeyChecking=no'` skips SSH's first-connection host verification, which is otherwise required for a freshly created VM Ansible has never connected to.

Run the playbook, passing the join token retrieved earlier and the master's URL as extra variables:

```bash
ansible-playbook -i inventory.ini join-k3s.yaml \
  -e k3s_url="https://<MASTER_IP>:6443" \
  -e k3s_token="<TOKEN>"
```

The playbook checks whether k3s is already installed on the target host before running the installation, so it's safe to run more than once.

Now, to verify that everything worked correctly, execute this command on the master:

```bash
kubectl get nodes
```

You should be able to see the new node.