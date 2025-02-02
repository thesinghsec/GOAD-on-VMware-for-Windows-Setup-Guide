---

<aside>
💡 This guide outlines the process of setting up a GOAD (Game Of Active Directory) lab environment on a Windows host using VMware. It includes troubleshooting steps for common errors encountered during setup and how to resolve them.

While the GOAD Active Directory lab is typically installed from a Linux host as stated on the GitHub pages, it is still feasible to set it up from a Windows host. This guide outlines the process of achieving this setup efficiently without resorting to nested virtualization, which could significantly impact performance.
</aside>

## Plan:

**Windows host:** with Vagrant installed to run the VMs on VMware.
**VMware Pro:** with Kali VM installed to run ansible playbooks to make the AD vulnerable.
[GOAD](https://github.com/Orange-Cyberdefense/GOAD/blob/main/ad/GOAD/README.md) : 5 VMs, 2 forests, 3 domains (full goad lab)

## Requirements:

### Download Vagrant:

<aside>
💡 Vagrant simplifies setting up and managing virtual development environments using simple text configuration files. It ensures consistency, isolation, and easy sharing of development environments across different machines.
</aside>

Link: https://developer.hashicorp.com/vagrant/install?product_intent=vagrant

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/818070fa-7aea-417b-b850-c21fb70c6800/fea14b0f-8d49-4a98-ad81-2a4d7af6d30f/Untitled.png)

- Open **PowerShell** and run below cmd:

```bash
vagrant plugin install vagrant-vmware-desktop
```

- Download and install **Vagrant VMware Utility.**

Link: https://developer.hashicorp.com/vagrant/install/vmware

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/818070fa-7aea-417b-b850-c21fb70c6800/25f6a0ef-1eec-4b00-a07a-6adbd8bb5000/Untitled.png)

- Run cmd to verify the successful installation of Vagrant.

```bash
vagrant --version
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/818070fa-7aea-417b-b850-c21fb70c6800/eb3c9bf8-c54d-43a4-b293-b2e967b118c3/Untitled.png)

- All done with Vagrant.

---
