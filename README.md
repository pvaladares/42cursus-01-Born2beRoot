# 42cursus-01-Born2beroot
This project aims to introduce you to the wonderful world of virtualization.


# 1. Virtual Machine (VirtualBox)

1 - On the 42 machine, launch the [Managed Software Center](img/VM/1.png) app and search/install [VirtualBox 5.2.20](img/VM/2.png). To be noted that at the time of writing the latest version is 6.1 as can be checked [here](https://www.virtualbox.org/). To be noted that the alternative software `UTM` stated on the subject cannot be used since there are no admin privileges to install it nor it is available on the `Managed Software Center` to download/install. So `VirtualBox` is indeed the mandatory software to be used on this project.

2 - [Download](https://www.debian.org/download) the latest stable version of Debian and place it on your `goinfre` user folder (since it is less restrictive on size limits).

3 - Step by step instructions to create VM
* Launch `VirtualBox`
* [Select](img/VM/3.png) `New` and type `Born2beRoot` as name, choose `Linux` type and `Debian (64-bit)` version.
* Leave [memory size](img/VM/4.png) as default `1024 MB`

4 - If doing the **bonus**, since there is a limitation with the 5.2.20 version use the workaround described below:
> Note: The 5.2.20 version that can be used at 42 has a [limitation/bug](https://www.virtualbox.org/ticket/18177) with impact on the bonus, since it will not be possible to set a disk with size 30.8G
  * Go to terminal, and still at `goinfre` user folder, type `VBoxManage createhd --filename Born2beRoot_DISK_31G54.vdi --size 31540 --format VDI`
  * Choose `Use an existing virtual hard disk file` and [select the newly created file](img/VM/5.png)
  * [Go to](img/VM/6.png) `Settings` and `Storage`, under `Storage Devices` choose `Empty` and then click on the "CD/Disk" icon on the right of the `Optical Drive` and select option `Choose Virtual Optical Disk File...`; [Select](img/VM/7.png) the debian ISO file that was privously saved on goinfre
 
 * Now just `Start` the VM to start the installation procedure of Debian.

# 2. Debian Installation

## 2.1 General
* [Select](img/Install/1.png) `Install` instead of any other option (remember, no graphical install is allowed)
* [Language](img/Install/2.png): select default `English`
* [Location](img/Install/3.png): select `other`, `Europe` and then `Portugal`
* [Local configuration](img/Install/4.png): select default `United States`
* [Keyboard](img/Install/5.png): `American English`
> The hostname of your virtual machine must be your login ending with 42 (e.g., wil42)
* [Hostname](img/Install/6.png): `pvaladar42`
* [Domain name](img/Install/7.png): *empty*
> You have to implement a strong password policy.
> 
> To set up a strong password policy, you have to comply with the following requirements:
> - (...)
> - Your password must be at least 10 characters long. It must contain an uppercase letter and a number. Also, it must not contain more than 3 consecutive identical characters.
> - The password must not include the name of the user.
* Root password: *see rules above* (use a strong password generator like [here](https://passwordsgenerator.net/))
> In addition to the root user, a user with your login as username has to be present.
* User account:
  * [Full name](img/Install/8.png): `Pedro Valadares`
  * [Username](img/Install/9.png): `pvaladar`
 * Password: *see rules above*
* [Timezone](img/Install/10.png): `Lisbon`

## 2.2 Disk partition

* For the disk there is a really nice tutorial [here](https://youtu.be/OQEdjt38ZJA?t=185).

## 2.3 Final installation steps

* Configure the package manager:
  * [Scan extra installation media](img/Install/11.png): choose `No`
  * [Debian archive mirror country](img/Install/12.png): choose `Portugal`
  * [Debian archive mirror](img/Install/13.png): choose `deb.debian.org`
  * [HTTP proxy information](img/Install/14.png): *empty*
* [Participate in the package usage survey](img/Install/15.png): choose `No`
* [Software selection](img/Install/16.png): *deselect all*
* Install the GRUB boot loader:
  * [Install the GRUB boot loader to your primary drive](img/Install/17.png): choose `Yes`
  * [Device for boot loader installation](img/Install/18.png): choose `/dev/sda`
* [Finish the installation](img/Install/19.png): choose `Continue`

## 2.4 Reboot, unlock the disk, login and check disk partitions

* Now the machine will reboot and the [GRUB boot loader will show the Debian](img/Install/20.png) and load it by default, if nothing is pressed
* Type the [unlock disk password](img/Install/21.png), previously set during the installation, to unlock the disk
* Then type the [username `pvaladar` and the associated password](img/Install/22.png)
* In order to cross-check the disk partition *versus* the subject (in this case the bonus), use the [`lsblk` utility](img/Install/23.png)

# 3. SSH

# 3.1 Installation
* Access super user privileges by typing `su` and entering the previously set password
* Install SSH by typing `apt install openssh-server -y`
* Make the following checks around openssh-server:
  * It is installed: `dpkg -l | grep ssh`
  * It is active (running): `systemctl status ssh`

# 3.2 Configuration
 
* Edit the configuration file using `vi` or `nano`, e.g.:  `nano /etc/ssh/sshd_config`
> A SSH service will be running on port 4242 only.
* Replace `# Port 22` by `Port 4242`
> For security reasons, it must not be possible to connect using SSH as root.


# Resources
* [Born2beRoot Correction](https://github.com/sltcestloic/born2beroot_correction/blob/master/correction_born2beroot.pdf)
