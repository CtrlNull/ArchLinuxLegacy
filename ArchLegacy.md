# Arch Linux Legacy Install

## Mirror list

~~~
// Check if you are connected to the internet
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

// Selection Menu
Select > dos
create select > primary > bootable > Write > yes > quit

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

$ locale-gen // set local

$ ln -sf /usr/share/zoneinfo/[region]/[city] /etc/localtime  // set clock of the system

$ hwclock --systohc --utc

clear
~~~

## Sys Details

~~~
$ echo [pcName] > /etc/hostname // Create hostname for computer

$ nano /etc/hosts > add these lines
~~~

127.0.1.1    localhost.localdomain pcName
Save file

~~~
$systemctl enable dhcpcd // setsup new password to arch

$passwd

$clear
~~~

## BootLoader

~~~
$ pacman -S grub // Setup GRUB bootloader

$ grub-install /dev/sda

$ grub-mkconfig -o /boot/grub/grub.cfg // configures grub loader

$ exit

$ unmount

$ reboot
~~~

## Login and set users

Login to arch

~~~
$ useradd -m -g users -G wheel -s /bin/bash [userName] // adds new arch user

$ passwd [userName] // addes password

$ EDITOR=nano visudo // goes into sudoers file

Find zwheel ALL=(ALL) ALL > uncomment

$ exit
~~~

## GUI and packages

login as new user

~~~
$ sudo pacman -S pulseaudio pulseaudio-alsa // install audio

$ sudo pacman -S xorg xorg-xinit // install graphics > select option (1) intergrated

$ clear

$ echo "exec gnome-session" > ~/.xinitrc // create a file of init for guid
$ sudo pacman -S gnome // install gnome desktop

// install random needed programs

$ startx // starts GUI
~~~

## Login manager

~~~
$ sudo pacman -S sddm // install login manager

$ sudo systemctl enable sddm.service // run login manager service

$ reboot
~~~

## Finished


