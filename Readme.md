
# Arch Linux :penguin: Legacy Install
![alt text]( "Logo Title Text 1")
---
Note** this is for non-dual boot, GNOME Setup

## Mirror list

~~~
// Check if you are connected to the interne
$ ping archlinux.org

// Update
$ pacman -Syy

// Download to update mirror list
$ pacman -S reflector -y

// Updates mirror list and places it in /etc~
$ reflector -c "US" -f -12 -l 10 -n 12 --save /etc/pacman.d/mirrorlist

~~~

## Partition HDD

~~~
// List disks
$ fdisk -l 

// Partition menu (like diskpart in windows)
$ cfdisk /dev/sda 
~~~

// Selection Menu
> Select > dos
> create select > primary > bootable > Write > yes > quit

~~~
// Formats partition
$ mkfs.ext4 dev/sda1 

// Mount Device
$ mount /dev/sda1 /mnt

// Check if disk is mounted
$ lsblk 

$ clear
~~~

## Install base system

~~~
// Install base system
$ pacstrap -i /mnt base base-devel 

// Generate fstab file
$ genfstab -U -p /mnt >> /mnt/etc/fstab 

// List file contents
$ cat /mnt/etc/fstab 

$ clear

// Login to system as root
$ arch-chroot /mnt /bin/bash
~~~

## TIME ZONE

~~~
// Set local of system
$ nano /etc/locale.gen  

//uncomment local you would like to use
or 
$ LANG=C perl -i -pe 's/#(en_US.UTF)/$1/' /etc/locale.gen

// set local
$ locale-gen 

// set clock of the system
$ localectl set-locale LANG="en_US.UTF-8"
 or
$ ln -sf /usr/share/zoneinfo/[region]/[city] /etc/localtime  

$ hwclock --systohc --utc

clear
~~~

## Sys Details

~~~
// Create hostname for computer
$ echo [pcName] > /etc/hostname 

$ nano /etc/hosts > add these lines
~~~

>127.0.1.1    localhost.localdomain pcName

Save file

~~~
// setsup new password to arch
$systemctl enable dhcpcd 

$passwd

$clear
~~~

## BootLoader

~~~
// Setup GRUB bootloader
$ pacman -S grub 

$ grub-install /dev/sda

// configures grub loader
$ grub-mkconfig -o /boot/grub/grub.cfg 

$ exit

$ unmount

$ reboot
~~~

## Login and set users

Login to arch

~~~
// adds new arch user
$ useradd -m -g users -G wheel -s /bin/bash [userName] 

// adds password
$ passwd [userName] 

// goes into sudoers file
$ EDITOR=nano visudo 

Find zwheel ALL=(ALL) ALL > uncomment

$ exit
~~~

## GUI and packages

login as new user

~~~
// install audio
$ sudo pacman -S pulseaudio pulseaudio-alsa 

// install graphics > select option (1) intergrated
$ sudo pacman -S xorg xorg-xinit 

$ clear

// create a file of init for guid
$ echo "exec gnome-session" > ~/.xinitrc 

// install gnome desktop
$ sudo pacman -S gnome 

// install random needed programs

// starts GUI
$ startx 
~~~

## Login manager

~~~
// install login manager
$ sudo pacman -S sddm 

// run login manager service
$ sudo systemctl enable sddm.service 

$ reboot
~~~

## Finished


