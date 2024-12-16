# debian-multistrap  

## Introduction  

This project takes a different approach compared to the typical debootstrap installation process.  
In my case, I wanted to create an x2go desktop server running Debian 12 with the XFCE desktop environment, the latest LibreOffice from the official website, and Google Chrome. You can, of course, add Firefox ESR or the latest stable version if you prefer. In the future, I may include the "new" Firefox repository in the build process.  

## The Script  

Some parts of the script are not perfect, but if you already have Debian installed in your preferred language and want to create a disk with the latest stable builds, this is for you.  
The script is based on various examples found online and refined through a lot of trial and error on my part.  

It automatically creates a backup of itself, so if you make changes to customize it for your preferences, you can easily revert to previous versions.  
With multistrap, all the software (except LibreOffice) is installed within the bootstrap environment. This ensures you start with the latest available software.  

## Handling Signatures  

Since current repositories require signatures, I've made adjustments to prevent multistrap from failing. Once the system is built, it uses proper signatures, so there’s no need to worry.  

## Cache Folder  

Because I ran the script multiple times in the same day, I got tired of re-downloading all the `.deb` packages repeatedly. To solve this, I used the `/var/cache/apt/archives` folder in the "cooking" environment and linked it to the target. Even if the target gets completely erased, the packages won’t need to be downloaded again.  

However, this might cause errors in multistrap if multiple versions of the same package are present. For this reason, the script deletes all cached packages at the start of the day.  

## Language and Installation within Chroot  

In multistrap, some packages are not fully configured, requiring manual fixes in the chroot environment or during the first real boot.  

Although I tried to automate language configuration entirely, using preseed answers was insufficient in some cases. The script pre-copies some "default" files from the local installation on the "cooking machine" to the target system. For example, I had to set the "universal" C language environment to avoid configuration errors. Without variables like `LC_ALL`, `LANGUAGE`, and `LANG`, errors would appear during `dpkg` or `tasksel` executions.  

## Using Tasksel in Chroot  

Even when I installed the same packages as a "real" installation, I found a bug related to powering off a VM using the "virtual power button." Some ACPI configurations were missing in multistrap. To fix this, I added a `tasksel install` step. While it doesn’t install new packages, it seems to reconfigure something.  

## LibreOffice Installation  

The script scrapes the LibreOffice website and downloads the necessary tar.gz files.  
It then extracts the files and prepares them for installation in the chroot environment. The installation runs in the background, allowing time to manually configure the sudo user and set its password.  

## Console Keyboard for Spanish/Latin American Layout  

I’m from Argentina, and many laptops use the LATAM keyboard. Debian has had a long-standing bug where console language files don’t work with the LATAM layout. To fix this, the script downloads and places the correct files where they belong, ensuring the keyboard works properly.  

## Fixes for X2Go  

X2Go has three major issues:  

1. It performs poorly when compositing is enabled in XFCE [**disabled**].  
2. Clicking in the top-right corner minimizes the X2Go session, which is inconvenient if you’re trying to close a window using the "X" button [**disabled**].  
3. Pressing `Ctrl + Alt + T` disconnects the session. This is problematic for me as I often open terminals this way [**disabled**].  

## Requirements  

- A live or installed Debian/Ubuntu-based environment to run the script.  
- A free drive (note: it will be formatted, and all data will be lost).  
- Internet access (a proxy is not implemented in this example).  

## Breakdown of the Script  

1. Create a script backup.  
2. Install dependencies for the script.  
3. Unmount `/dev/vdb`.  
4. Set up the partition table to GPT (UEFI).  
5. Create the EFI partition.  
6. Create the OS partition.  
7. Format the partitions.  
8. Mount the OS partition.  
9. Create directories in `/tmp/installing-rootfs`.  
10. Download and install X2Go keyring in `/tmp/installing-rootfs`.  
11. Download and install Google Chrome keyring in `/tmp/installing-rootfs`.  
12. Create a configuration file for multistrap.  
13. Run multistrap to build the system.  
14. Configure the network settings.  
15. Mount the EFI partition.  
16. Generate the `fstab` file.  
17. Prepare the system for chroot.  
18. Download LibreOffice tar.gz files and extract them.  
19. Set keyboard maps for non-graphical consoles.  
20. Copy skeleton files, default settings, and crontabs to the target system.  
21. Disable compositing in XFCE for X2Go.  
22. Generate the `rc.local` file for simple startup scripts.  
23. Enter the chroot environment.  
24. Set up additional packages in the chroot.  
25. Install GRUB bootloader.  
26. Add a local user with a custom username and password.  
27. Install LibreOffice and its language pack.  
28. Generate system locales.  
29. Disable unnecessary services like `ldm`.  
30. Unmount `/dev/vdb`.  

**End of the road! Keep up the good work!**  
