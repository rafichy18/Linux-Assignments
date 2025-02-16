# Linux Management
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


# APT Package Management Assignment

## **Part 1: Understanding APT & System Updates**

### **1. Check APT Version**
```bash
apt --version
# output
apt --version
apt 2.7.14 (amd64)
![](![apt version](https://github.com/user-attachments/assets/0cb9bf12-9ce7-4a68-90d6-7d242a1f628b)

### **2. Update the Package List**
```bash
sudo apt update
```
**Explanation:** This command fetches the latest package lists from configured repositories, ensuring we get the latest versions and security updates.

### **3. Upgrade Installed Packages**
```bash
sudo apt upgrade -y
```

### **4. View Pending Updates**
```bash
apt list --upgradable
```
rafi@lab-robotics:~$ apt list --upgradable
Listing... Done

## **Part 2: Installing & Managing Packages**

### **1. Search for an Image Editor**
```bash
apt search image editor
**Screenshoot of selected package**
![](![package name](https://github.com/user-attachments/assets/0864d660-b810-4566-b7bd-89af14d51f6d)


### **2. View Package Details**
apt show zim
Package: zim
Version: 0.75.2-1
Priority: optional
Section: universe/x11
Origin: Ubuntu
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Original-Maintainer: Zim Package Maintainers <zim@packages.debian.org>
Bugs: https://bugs.launchpad.net/ubuntu/+filebug
Installed-Size: 5151 kB

### **3. Install the Package**
```bash
sudo apt install zim  -y
```
**Installation Confirmation:** _ rafi@lab-robotics:~$ apt list --installed | grep zim

No VM guests are running outdated hypervisor (qemu) binaries on this host.
rafi@lab-robotics:~$ apt list --installed | grep zim

WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

zim/noble,now 0.75.2-1 all [installed]

---
## **Part 3: Removing & Cleaning Packages**

### **1. Uninstall the Package**
```bash
sudo apt remove gimp -y
```
**Is the package fully removed?**  _(No, configuration files remain.)_  

### **2. Remove Configuration Files**
```bash
sudo apt purge zim -y
```
**Difference between `remove` and `purge`:**  
- `remove`: Uninstalls the package but keeps configuration files.
- `purge`: Completely removes the package along with configuration files.

### **3. Remove Unused Dependencies**
```bash
sudo apt autoremove -y
```
**Why is this step important?**  
- It removes packages that were installed as dependencies but are no longer needed.

### **4. Clean Up Downloaded Package Files**
```bash
sudo apt clean
```
**What does this command do?**  
- It clears cached `.deb` files to free up disk space.

---
## **Part 4: Managing Repositories & Troubleshooting**

### **1. List All APT Repositories**
```bash
cat /etc/apt/sources.list
```
**Observations:** _(This file contains the list of repositories from which APT retrieves packages.)_  
**Screenshoot**


### **2. Add a New Repository (Universe Repository)**
```bash
sudo add-apt-repository universe
sudo apt update
```
**What does the universe repository contain?**
It includes community-maintained open-source software.
**Types of Packages in Universe Repository:** 
)_  

### **3. Simulate an Installation Failure**
```bash
sudo apt install fakepackage
```
**Error Message:** _(E: Unable to locate package fakepackage)_  

### **4. Troubleshooting the Issue**
- **Check for typos** in the package name.
- Run `sudo apt update` to refresh the package list.
- Search for available packages using `apt search <keyword>`.
- Check if additional repositories are needed.

---
## **Bonus Challenge: Using `apt-mark`**

### **Hold a Package** (Prevent it from being updated)
```bash
sudo apt-mark hold zim
```
### **Unhold a Package** (Allow updates again)
```bash
sudo apt-mark unhold zim
```
**Why would you hold a package?**  
- To prevent a specific package from being updated due to compatibility or stability reasons.

---
Depends: python3-xdg, python3:any, python3-gi, gir1.2-gtk-3.0, xdg-utils



