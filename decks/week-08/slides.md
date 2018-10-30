### Virtualization

> Virtualization enables running multiple operating system instances concurrently on the same physical machine.


### Virtualization
- Virtualization software manages computing resources (CPU, memory, and I/O) and their use among **guest** operating systems.
- Virtualization increases efficiency because the hardware is utilized to handle multiple guests simultaneously.
- Guest operating systems are isolated from each other and access the hardware through the hypervisor.


### Virtualization and Hypervisors
  - A **Hypervisor** is a software layer that sits between the virtual machines (VMs) and the underlying hardware to handle sharing resources among guest operating systems.
  - For example, you can have Linux (CentOS, Ubuntu, etc.), Unix (FreeBSD), and Windows running alongside.
  - Examples of Hypervisors include Oracle VirtualBox, VMware ESXi, and the Xen Project.


### Machine Image
A machine image is a single static unit that contains a pre-configured operating system and installed software packages which are used to create new running machines.


### The Works on my Machine Problem (I)
- One common problem in software development is "works on my machine" phenomenon.
- Many developers set up a development environment with tools and libraries.
- The environment grows up over time with more added libraries and more changes to configuration options.



### The Works on my Machine Problem (II)
- The local development environment becomes very different from the target production environment.
- Libraries that are present on the development system may not exist on the production system.
- This leads into an unexpected errors and runtime behaviors.


### Solutions to the Works on my Machine Problem
- Create an isolated, dedicated development environment locally for each project that matches the production environment.
  - **Option 1**: Provision a custom VM with all the required development environment locally using virtualization software.
  - **Option 2**: Develop in a more managed, smaller, and isolated environment such as a _Container_ environment.



### Infrastructure as Code Approach
- All the previous solutions are central to the **infrastructure as code** approach.
- Infrastructure as code is the practice of managing and provisioning OS environments through machine-readable definition files, rather than manually applying changes to VM images and installing dependency libraries and tools.



### Creating and Managing Custom Virtual Machine Images
- There're many virtualization systems that facilitate creating and managing virtual machine images.
  -  vSphere, the VMware virtualization suite of products.
- There're special tools for building and managing portable virtual machine images and environments.
  - [Vagrant](https://www.vagrantup.com/)
  - [Packer](https://packer.io)
  


### Vagrant
- Vagrant is an open source tool for provisioning and managing virtual machine environments.
- Vagrant can manage development environments running on a local virtualized platform such as VirtualBox or VMware, in the cloud via AWS, Azure, or any other provider, or in containers such as Docker.



### Vagrant: Getting Started (I)
1. Install a hypervisor such as Oracle VirtualBox.
2. [Install Vagrant](https://www.vagrantup.com) on your local environment.
3. You will need to pick a Vagrant Box, the package format for Vagrant environments.
  - Boxes can be installed locally from an image or from the [publicly available catalog of Vagrant boxes](https://vagrantcloud.com/boxes/search). 



### Vagrant: Getting Started (II)
- You will need to use the following commands:
  - `vagrant init <name_of_vm_image>`
  - `vagrant up`
  - `vagrant ssh`


###  Using Vagrant (I)
- First Command:
```bash
$ vagrant init centos/7
```
  - The command above will create a file called _Vagrantfile_ that contains all the provisioning  options to customize your VM (e.g., the amount of memory on the VM).



###  Using Vagrant (II)
- Second Command:
```bash
$ vagrant up
```
  - The command above will download, start, and provision the vagrant VM environment.



###  Using Vagrant (III)
- Third Command:
```bash
$ vagrant ssh
```
  - The command above will connect to the local VM from the host OS via SSH
- To shut down the VM instance, use the command `vagrant halt`


### Vagrant Demo



### Packer (I)

- [Packer](https://packer.io/) is an open source tool for building virtual machine images for multiple platforms from a single configuration file.
- Packer can be used to generate new machine images for multiple platforms with the changes made to them.
- This is in particular helpful in keeping development and production environments identical.



### Packer (II)
- To create an image, Packer launches a VM instance from a source image of your choice.
- Packer can customize the VM instance by running commands and scripts that may install libraries or customize configuration files.
- Finally, packer saves a copy of the Virtual Machine's state as an image.


### Packer (II)
- Packer uses a template configuration file in JSON format.
- Packer's template file defines how to create an image, add provisioning options, and install software and libraries for the image.
- To build the custom image, run the command `packer build <custom_image.json>`



### Packer: Getting Started
1. Download the Packer binary file from [https://packer.io](https://packer.io/)
2. Create a packer template file
3. Run 

```bash
$ packer build
```


### Packer: Demo

