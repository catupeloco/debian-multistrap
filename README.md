# debian-multistrap
----Introduction
This project is a different aproach of the typical debootstrap installation process.
In my case I've wanted to make a x2go desktop server running debian 12, xfce desktop, the lastest libreoffice from website and as my preference Google Chrome. You can add the firefox-esr or the lastest stable of course if you like. In a future I may add the "new" firefox repo in the build process.

----The script
The are some parts in the script that are not perfect but if you have a debian already installed in your language and want to make a disk with the latest stable builds this is for you. The script is based on several examples found on the open web and a lot of trial and error by my self.
It will automaticaly make a backup of it self, so if you are changing staff to fit your preferences you can easily go back to previous versions.
With multistrap all the software (but libreoffice) is installed within the bootstrap environment so in the first go you have all the lastest software available.

----Signature stuff
As current repositories require signature staff, I've twisted things to avoid multistrap to fail. Afterwards the built system makes use of real signatures, so don't worry.

----Cache folder
Because I've runned the script a lot in the same day I was tired of downloading all the deb packages again and again. So I've used /var/cache/apt/archives folder in the "cooking" environment and the "cooking" target as a link so even if the target is totally ereased all the packages wont be downloaded again and again.
This could lead to errors on multistrap if various versions of the same packages are in the folder, so for sanity the script will erase all packages at the first run of the day.




----Requirements:
A live or local debian/ubuntu base environment for running the script.
A free drive (beware that it will be formated and all data will be lost)
Access to internet (you may use proxy but in this example is not implemented)

----Brake down of the differents parts of the script.

Making script backup 

Installing dependencies for this script 

Unmounting /dev/vdb  

Setting partition table to GPT (UEFI) 

Creating EFI partition 

Creating OS partition 

Formating partitions 

Mounting OS partition 

Downloading x2go and Google Chrome keyrings 

---------Creating Directories in /tmp/installing-rootfs

---------Installing x2go keyring here

---------Installing x2go keyring in /tmp/installing-rootfs

---------Installing chrome keyring here

---------Installing chrome keyring in /tmp/installing-rootfs

Creating configuration file for multistrap 

Running multistrap 

Configurating the network 

Mounting EFI partition 

Generating fstab 

Getting ready for chroot 

Downloading Libreoffice 

Setting Keyboard maps for non graphical console 

Copying skel, defaults and crontab 

Fixing XFCE on X2Go by disabling compositing 

Generating rc.local for simple start up scripts 

Entering chroot 

Setting up additional packages 

Installing grub 

Adding local user 

What username do you want?: username

New password: 

Retype new password: 

passwd: password updated successfully

Installing LibreOffice and its language pack 

LibreOffice X.X.X.X installation done.

Listing relevant packages 

[removed part as it has 'today' versions]

Setting languaje 

Current default time zone: 'America/Argentina/Buenos_Aires'

Local time is now:      Sat Oct 26 01:21:52 -03 2024.

Universal Time is now:  Sat Oct 26 04:21:52 UTC 2024.


Generating locales (this might take a while)...

  es_AR.UTF-8... done
  
Generation complete.

Generating locales (this might take a while)...

  es_AR.UTF-8... done
  
Generation complete.

LANG=C

LANGUAGE=C

LC_CTYPE="C"

LC_NUMERIC="C"

LC_TIME="C"

LC_COLLATE="C"

LC_MONETARY="C"

LC_MESSAGES="C"

LC_PAPER="C"

LC_NAME="C"

LC_ADDRESS="C"

LC_TELEPHONE="C"

LC_MEASUREMENT="C"

LC_IDENTIFICATION="C"

LC_ALL=C

Disabling ldm 

Unmounting /dev/vdb 

END of the road!! keep up the good work
