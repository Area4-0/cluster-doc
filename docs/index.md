#Introduction

Cluster 4.0 provides a set of machines to be used to run research experiments.
These machines are located in the campus of Cesena.
Their resources are shared among all students and researchers, and exploitable through [Proxmox](https://pve.proxmox.com/pve-docs/chapter-pve-gui.html) web interface.
The goal of this infrastructure is to offer isolated and flexible computational resources to multiple research teams.

The system is designed to:

- Ensure isolation between research groups
- Allow users to manage their own resources independently
- Prevent accidental interference with other users’ workloads

No prior experience with Proxmox is required, although basic familiarity with Unix-like systems and virtualization is recommended.

Proxmox is a virtualization platform that allows users to create and manage:

- **Virtual Machines (VMs)**: Full operating systems running on virtual hardware
- **Containers (LXC)**: Lightweight environments sharing the host kernel

Through the web interface, users can deploy, monitor, and control these resources.

The cluster is organized using resource pools.
Each research group (or supervisor) is assigned a dedicated resource pool.
Users can only interact with resources inside their own resource pool.

!!! seealso
    To use this service, please read the [quickstart section](./quickstart.md).

!!! note
    The machines are not accessible from the outside network, you need to be connected to the **campus of Cesena's VPN** network to access them.

!!! note
    Machines' resources are shared among all researchers, so unused containers should be removed to leave resources available to other users.
