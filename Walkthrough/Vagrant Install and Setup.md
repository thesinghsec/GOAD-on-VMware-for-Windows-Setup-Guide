# Setup Vagrant:
💡 This guide outlines the process of setting up a GOAD (Game Of Active Directory) lab environment on a Windows host using VMware. It includes troubleshooting steps for common errors encountered during setup and how to resolve them.

While the GOAD Active Directory lab is typically installed from a Linux host as stated on the GitHub pages, it is still feasible to set it up from a Windows host. This guide outlines the process of achieving this setup efficiently without resorting to nested virtualization, which could significantly impact performance.

## Plan:

- **Windows host:** with Vagrant installed to run the VMs on VMware.
- **VMware Pro:** with Kali VM installed to run Ansible playbooks to make the AD vulnerable.
- **[GOAD](https://github.com/Orange-Cyberdefense/GOAD/blob/main/ad/GOAD/README.md):** 5 VMs, 2 forests, 3 domains (full GOAD lab).

## Requirements:

### Download Vagrant:

💡 Vagrant simplifies setting up and managing virtual development environments using simple text configuration files. It ensures consistency, isolation, and easy sharing of development environments across different machines.

**Link:** [Download Vagrant](https://developer.hashicorp.com/vagrant/install?product_intent=vagrant)

![image](https://github.com/user-attachments/assets/d70ab319-e0ae-42a3-a94d-bd56cb9247d6)

- Open **PowerShell** and run the following command:

  ```bash
  vagrant plugin install vagrant-vmware-desktop
  ```
- Download and install Vagrant VMware Utility.
  - Link: [Vagrant VMware Utility](https://developer.hashicorp.com/vagrant/install/vmware)
   ![image](https://github.com/user-attachments/assets/e806f451-e529-4b96-a8d0-8da382eed2bd)

- Run cmd to verify the successful installation of Vagrant.
  ```bash
  vagrant --version
  ```
  ![image](https://github.com/user-attachments/assets/db09eb54-1819-4c54-b73b-ebb91f816dab)

- All done with Vagrant.
