# debian-multistrap
----Introduction:

This project has a different aproach of typical debootstrap installation process.
In my case I've wanted to make an x2go desktop server running debian 12, xfce desktop, the lastest libreoffice from website and Google Chrome. You may add the firefox-esr or the lastest stable of course if you like. In a future I may add the "new" firefox repo in the build process.

----The script:

The are some parts in the script that are not perfect but if you have a debian already installed in your language and want to make a disk with the latest stable builds this is for you. The script is based on several examples found on the open web and a lot of trial and error by my self.
It will automaticaly make a backup of it self, so if you are changing staff to fit your preferences you can easily go back to previous versions.
With multistrap all the software (but libreoffice) is installed within the bootstrap environment so in the first go you have all the lastest software available.

----Signature stuff

As current repositories require signature staff, I've twisted things to avoid multistrap to fail. Afterwards the built system makes use of real signatures, so don't worry.

----Cache folder

Because I've runned the script a lot in the same day I was tired of downloading all the deb packages again and again. So I've used /var/cache/apt/archives folder in the "cooking" environment and the "cooking" target as a link so even if the target is totally ereased all the packages won't be downloaded again and again.
This could lead to errors on multistrap if various versions of the same packages are in the folder, so for sanity the script will erase all packages at the first run of the day.

----Language and installing within chroot

In multistrap it seems that some packages are not fully configurated, you may need to fix some on chroot or first real boot.
Even if I wanted to fully automate the language configuration, in some cases the use of preseed answers was not enough, so the script precopy some "defauls" files from local installation on "cooking machine" to target. Another example of "language" fixes was the "universal" C language I had to put to avoid configuration errors. This was because if variables like "LC_ALL, LANGUAGE, LANG" were not set some errors were shown on screen when dpkg or tasksel ran.

----Use of tasksel on chroot

Even if I install all same packages from a "real" installation I've detected a bug on powering off vm from "virtual power button". Some ACPI stuff wasn't been done on multistrap. To fix this I've added a step of "tasksel install" that makes some unknow magic. This doesn't really installs a package but it may reconfigure something.

----Libreoffice installation

In a few lines this script scraple libreoffice web page and downloads locally the tar.gz files. Next it decompress both files and set them ready for installation on chroot. The installation runs in background so in the meantime I could manually set sudo user and its password. Then it waits to finish.

----Console spanish/latin keyboard

I'm from Argentina, so laptops use the latam keyboard. Debian has a long time bug that some files for console lenguage doesn't work in latam keyboard. So for this I download the files and put them where they should be in the first place and then it simply works.

----X2Go fixes

X2go has 3 mayor bugs
1) It works awful when composing is enabled on xfce [disabled]
2) When you put your mouse cursor on the top right corner and you clic it, x2go minimize it self. This is insane when you just want to close a window with the normal X [disabled]
3) When you press Control + Alt + T it disconnects. For me this is also insane as I open terminal this way all the time. [disabled]

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
