# Linux Management
### Assignment 1
# Account Setup
In the first step, I have created a Microsoft Azsure account using our university email address. Then, my microsoft azsure account is successfully created and I have recevied $100 worth of credit which helps me to purchase different types of useful learning environment.

# Create Virtual Machine
I have created a virtual machine where I can learn and do some projects for this course.
Then, I named the machine "lab-robotics" and then I have select the no infrastructure redundancy required option and Trusted launch virtual machines security type.
I choosed Ubuntu Server 24.04 LTS - x64 Gen2 server and B series version 2 which is Standard_B21s_v2.
After completing all the steps, I got a key and I have selected the connect option and choose the native ssh option.
There is a copy and execute SSH command button, I have pasted the key which I have got earlier.
Then open the windows powershell and paste the link generated link there and I reached in the Linux virtual machine.
![](![Linux assignment 1](https://github.com/user-attachments/assets/750a37e0-b9c1-4575-bb3a-4303cce03926)



## APT Package Management Assignment

## **Part 1: Understanding APT & System Updates**

### **1. Check APT Version**
```bash
apt --version
```
**Output:**  _(apt --version
apt 2.7.14 (amd64)

### **2. Update the Package List**
```bash
sudo apt update
```
**Explanation:** This command fetches the latest package lists from configured repositories, ensuring we get the latest versions and security updates.

### **3. Upgrade Installed Packages**
```bash
sudo apt upgrade -y
```
**Difference between `update` and `upgrade`:**  
- `update`: Refreshes the package list but doesn’t install updates.
- `upgrade`: Installs the latest versions of all packages listed in the updated package list.

### **4. View Pending Updates**
```bash
apt list --upgradable
```
Pending Updates:  rafi@lab-robotics:~$ apt list --upgradable
Listing... Done
---
## **Part 2: Installing & Managing Packages**

### **1. Search for an Image Editor**
```bash
apt search image editor
```
**Selected Package:**  zim 
### **2. View Package Details**
```bash
apt show zim
```

**Output (Key Information)**

rafi@lab-robotics:~$ apt show zim
Package: zim
Version: 0.75.2-1
Priority: optional
Section: universe/x11
Origin: Ubuntu
Bugs: https://bugs.launchpad.net/ubuntu/+filebug
Installed-Size: 5151 kB
Depends: python3-xdg, python3:any, python3-gi, gir1.2-gtk-3.0, xdg-utils
Recommends: gir1.2-gtkspell3-3.0
Suggests: bzr, git, mercurial, fossil, graphviz, ditaa, scrot, dvipng, gir1.2-gtksource-3.0, python3-zeitgeist, r-base, gnuplot, lilypond
Homepage: https://zim-wiki.org
Download-Size: 1215 kB
APT-Sources: http://azure.archive.ubuntu.com/ubuntu noble/universe amd64 Packages
Description: graphical text editor based on wiki technologies

What dependencies does it require?

python3
python3-gtk-3.0
gir1.2-gtk-3.0

### **3. Install the Package**
```bash
sudo apt install zim -y
```
### **4. Check Installed Package Version
apt list --installed | grep zim
### Part 3: Removing & Cleaning Packages
**1. Uninstall the Package
sudo apt remove zim -y

### Screenshot
![](![Screenshot_13](https://github.com/user-attachments/assets/13e1ad2c-121e-4423-9d9e-b2c498629ca4)

** Is the package fully removed?
- No, the configuration files are still on the system.
### ** 2. Remove Configuration Files
sudo apt purge zim -y

### Screenshot
![](![Screenshot_15](https://github.com/user-attachments/assets/d7432b5d-66a1-435e-bb59-6440fc5a95ae)


# Difference between remove and purge:

- Remove: Deletes the package but keeps configuration files.
- Purge: Deletes both the package and its configuration files.

# 3. Clear Unnecessary Package Dependencies
sudo apt autoremove -y
# Why is this step important?

- It removes unneeded dependencies that were installed automatically.
- Frees up disk space.
### 4. Clean Up Downloaded Package Files
sudo apt clean
# What does this command do?

- It removes cached package files from /var/cache/apt/archives.
- Helps free up disk space.
### Part 4: Managing Repositories & Troubleshooting
*** 1. List All APT Repositories
cat /etc/apt/sources.list

### What do you notice in this file?

- It contains a list of repositories (deb or deb-src lines).
- Lists sources where packages are downloaded from.
# 2. Add the Universe Repository
sudo add-apt-repository universe
sudo apt update
# What types of packages are found in the universe repository?

- Community-maintained software, not officially supported by Ubuntu.
# 3. Simulate an Installation Failure and Troubleshoot
sudo apt install fakepackage
*** Output:
E: Unable to locate package fakepackage
# How would you troubleshoot this issue?

- Verify that the package name is correct.
- Run sudo apt update to refresh package lists.
- Check if the package is in the enabled repositories.
# Bonus Challenge (Optional)
# Hold a Package
sudo apt-mark hold zim
# Why would you want to hold a package?

- To prevent updates that might break compatibility.
### Unhold a Package
sudo apt-mark unhold zim
![](![Screenshot_14](https://github.com/user-attachments/assets/42e32051-006b-4ea8-959c-31c4717498d4)



# Linux Virtualization Exercise

## Introduction

This report documents the steps taken to complete the Linux Virtualization exercise on an Ubuntu 24.04 system with nested virtualization enabled. It covers Multipass, LXD, Docker, and Snapcraft.

# Part 1: Virtualization Concepts

### Research on Virtualization Concepts

Virtualization enables running multiple operating systems or applications on the same physical machine using a hypervisor. There are two main types of virtualization:

Full Virtualization (VMs): Uses a hypervisor to emulate hardware and run multiple OS instances.

Container-Based Virtualization: Uses OS-level isolation to run multiple applications in isolated user spaces.

# Part 2: Working with Multipass

# Installing Multipass

```bash
sudo snap install multipass
```
### Basic Multipass Commands

### Launching a Default Ubuntu Instance
```bash
multipass launch --name test-vm
```
### Listing Instances
```bash
multipass list
```
### Accessing the Instance Shell
```bash
multipass shell test-vm
```
### Cloud-init Configuration

### Created a cloud-init.yaml file:
```bash
#cloud-config
package_update: true
packages:
  - nginx
  - htop
users:
  - name: student
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
```
### Screenshot 
![](![Screenshot_20](https://github.com/user-attachments/assets/4d18972c-b951-4c04-a870-0fea7f464a6d)
![](![Screenshot_24](https://github.com/user-attachments/assets/f5c4a2b3-7eb2-4b6d-b691-b8a9cbbcaed0)


### Launching a Multipass VM with Cloud-Init
```bash
multipass launch --name my-cloud-vm --cloud-init cloud-init.yaml
```
### Verifying Nginx Installation
```bash
multipass shell my-cloud-vm
systemctl status nginx
```
# Screenshot
![](![Screenshot_19](https://github.com/user-attachments/assets/38061053-fe2f-40c0-b978-96ff2f174907)

# Part 3: Exploring LXD

### Installing and Initializing LXD
```bash
sudo apt update
sudo apt install -y lxd
```
### Creating container
```bash
lxc launch ubuntu:20.04 my-container
lxc list
lxc exec my-container -- bash
lxc stop my-container
lxc delete my-container
```
# Screenshot
![](![Screenshot_21](https://github.com/user-attachments/assets/62f41915-75c1-48de-8da0-c57d66f23d2a)


### Part 4: Working with Docker

# Installing Docker
# Installing and Initializing LXD
# Installing and Initializing LXD
```bash
sudo apt update
sudo apt install -y docker.io
sudo systemctl enable --now docker
```
# Creating a Simple Dockerfile
### Installing and Initializing LXD
```bash
FROM ubuntu:20.04
RUN apt update && apt install -y nginx
CMD ["nginx", "-g", "daemon off;"]
```

### Screenshot
![](![Screenshot_22](https://github.com/user-attachments/assets/5d3d281c-615d-41eb-9320-0a71fb8abe85)


# Part 5: Working with Snaps
### Installing Snapcraft
```bash
sudo snap install snapcraft --classic
```
# Packaging a Simple App into a Snap
### Created a snapcraft.yaml file:
```bash
name: my-snap
base: core20
version: '1.0'
summaries: My first snap
architectures: [amd64]
apps:
  my-app:
    command: echo "Hello, Snap!"
```
# Screenshot
![](![Screenshot_23](https://github.com/user-attachments/assets/2033e688-6226-4d0f-93ef-7072b7f6facf)
