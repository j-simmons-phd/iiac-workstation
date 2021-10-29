# Immutable Infrastructure as Code Workstation

The Immutable Infrastructure as Code Workstation project bootstraps your localhost for developing Immutable Infrastructure as Code (IIaC). The IIaC toolchain is built around Ansible, which must be installed manually before you begin (see **Prerequisites**), and as such the workstation is designed to be run from Linux.  Windows 11 users can use the Windows Linux Subsystem v2 (WSL2) and its support for GUI apps to run the IIaC toolchain (with a little assistance from [Chocolatey](https://chocolatey.org/).

The full provided IIaC toolchain is as follows:

- [Ansible](https://www.ansible.com/), including [pywinrm](https://github.com/diyan/pywinrm) for developing Windows images *base version installed manually, see **Prerequisites***
- [VirtualBox](https://www.virtualbox.org/) *Windows 11 users, see see **Prerequisites***
- [Docker](https://www.docker.com/) *Windows 11 users, see see **Prerequisites***
- [Vagrant](https://www.vagrantup.com)
- [Terraform](https://www.terraform.io/)
- [Packer](https://www.packer.io/)
- [Visual Studio Code](https://code.visualstudio.com/), including plugins for Docker, Vagrant, Terraform, Packer, and Ansible
- [Git](https://git-scm.com/)
- Vim language support for Docker, Vagrant, Terraform, Packer, and Ansible

## Prerequisites

All users must install Ansible manually before proceeding.  Windows 11 users have some additional steps to perform to set up a WSL2 Ubuntu environment for use with the IIaC toolchain.

**Note: Once the Windows 11 specific steps are complete, all instructions assume Windows 11 users are operating from within their WSL2 Ubuntu environment.**

### Windows 11 Users

Ansible only runs under Unix-like operating systems, so Windows 11 users must operate within a WSL2 Ubuntu environment.  Further, a WSL Ubuntu environment cannot run VirtualBox or Docker.  So, these two tools must also be installed before proceeding with the Ansible install.  We will use Chocolatey to facilitate these installations.

1. [Install Chocolatey](https://chocolatey.org/install)
1. Install VirtualBox by running `choco install virtualbox` from an elevated command prompt, verify it installed correctly by launching from the Start Menu
1. Install Docker by running  `choco install docker-desktop` from an elevated command prompt, verify it installed correctly by launching from the Start Menu and accepting the license
1. Ensure the WSL2 is installed and up to date
    1. Determine if WSL2 is installed by running `wsl --status` from an elevated command prompt
    1. If WSL2 is not installed, install it by running `wsl --install` from an elevated command prompt
    1. If WSL2 is installed, update it by running `wsl --update` from an elevated command prompt
1. Install WSL2 Ubuntu environment from the **Microsoft Store** by launching the **Microsoft Store**, searching for Ubuntu and clicking the **Get** button, then launch it from the start menu and follow prompts to create your Ubuntu user

### Install Ansible

Follow the official [Installing Ansible on specific operating systems](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-specific-operating-systems) instructions to install Ansible.  Windows 11 users, remember to follow these instructions in your WSL2 Ubuntu environment.

## Install IIaC Toolchain

Note, these instructions are for all users, including Windows 11 running inside a WSL2 environment.

1. Download the requirements.yaml file to your computer by running `wget https://raw.githubusercontent.com/j-simmons-phd/iiac-workstation/main/requirements.yaml`
1. Download the iiac-workstation.yaml file to your computer by running `wget https://raw.githubusercontent.com/j-simmons-phd/iiac-workstation/main/iiac-workstation.yaml`
1. Install the requirements by running `ansible-galaxy install -r requirements.yaml`
1. Execute the playbook by running `ansible-playbook -i,localhost --ask-become-pass ./iiac-workstation.yaml`

