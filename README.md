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
Making script backup ----------------------------------------
Installing dependencies for this script ---------------------
Unmounting /dev/vdb  ----------------------------------------
Setting partition table to GPT (UEFI) -----------------------
Creating EFI partition --------------------------------------
Creating OS partition ---------------------------------------
Formating partitions ----------------------------------------
Mounting OS partition ---------------------------------------
Downloading x2go and Google Chrome keyrings -----------------
---------Creating Directories in /tmp/installing-rootfs
---------Installing x2go keyring here
---------Installing x2go keyring in /tmp/installing-rootfs
---------Installing chrome keyring here
---------Installing chrome keyring in /tmp/installing-rootfs
Creating configuration file for multistrap ------------------
Running multistrap ------------------------------------------
Configurating the network -----------------------------------
Mounting EFI partition --------------------------------------
Generating fstab --------------------------------------------
Getting ready for chroot ------------------------------------
Downloading Libreoffice -------------------------------------
Setting Keyboard maps for non graphical console -------------
Copying skel, defaults and crontab --------------------------
Fixing XFCE on X2Go by disabling compositing ----------------
Generating rc.local for simple start up scripts -------------
Entering chroot ---------------------------------------------
Setting up additional packages ------------------------------
Installing grub ---------------------------------------------
Adding local user -------------------------------------------
What username do you want?: jgalvez
New password: 
Retype new password: 
passwd: password updated successfully
Installing LibreOffice and its language pack ----------------
LibreOffice 24.8.2 installation done.
Listing relevant packages -----------------------------------
||/ Name                                               Version                                   Architecture Description
+++-==================================================-=========================================-============-=======================================
ii  google-chrome-stable                               130.0.6723.69-1                           amd64        The web browser from Google
ii  libobasis24.8-base                                 24.8.2.1-1                                amd64        Base module for LibreOffice 24.8.2.1
ii  libobasis24.8-calc                                 24.8.2.1-1                                amd64        Calc module for LibreOffice 24.8.2.1
ii  libobasis24.8-core                                 24.8.2.1-1                                amd64        Core module for LibreOffice 24.8.2.1
ii  libobasis24.8-draw                                 24.8.2.1-1                                amd64        Draw module for LibreOffice 24.8.2.1
ii  libobasis24.8-en-us                                24.8.2.1-1                                amd64        Language module for LibreOffice 24.8, language en_US.2.1
ii  libobasis24.8-es                                   24.8.2.1-1                                amd64        Language module for LibreOffice 24.8, language es.2.1
ii  libobasis24.8-extension-beanshell-script-provider  24.8.2.1-1                                amd64        Script provider for BeanShell extension for LibreOffice 24.8.2.1
ii  libobasis24.8-extension-javascript-script-provider 24.8.2.1-1                                amd64        Script provider for JavaScript extension for LibreOffice 24.8.2.1
ii  libobasis24.8-extension-mediawiki-publisher        24.8.2.1-1                                amd64        MediaWiki publisher extension for LibreOffice 24.8.2.1
ii  libobasis24.8-extension-nlpsolver                  24.8.2.1-1                                amd64        NLPSolver extension for LibreOffice 24.8.2.1
ii  libobasis24.8-extension-pdf-import                 24.8.2.1-1                                amd64        PDF import extension for LibreOffice 24.8.2.1
ii  libobasis24.8-extension-report-builder             24.8.2.1-1                                amd64        Report Builder extension for LibreOffice 24.8.2.1
ii  libobasis24.8-firebird                             24.8.2.1-1                                amd64        Firebird module for LibreOffice 24.8.2.1
ii  libobasis24.8-gnome-integration                    24.8.2.1-1                                amd64        GNOME integration module for LibreOffice 24.8.2.1
ii  libobasis24.8-graphicfilter                        24.8.2.1-1                                amd64        Graphic filter module for LibreOffice 24.8.2.1
ii  libobasis24.8-images                               24.8.2.1-1                                amd64        Images module for LibreOffice 24.8.2.1
ii  libobasis24.8-impress                              24.8.2.1-1                                amd64        Impress module for LibreOffice 24.8.2.1
ii  libobasis24.8-kde-integration                      24.8.2.1-1                                amd64        KDE integration module for LibreOffice 24.8.2.1
ii  libobasis24.8-librelogo                            24.8.2.1-1                                amd64        LibreLogo toolbar for LibreOffice 24.8 Writer.2.1
ii  libobasis24.8-libreofficekit-data                  24.8.2.1-1                                amd64        Libreofficekit data files for LibreOffice 24.8.2.1
ii  libobasis24.8-math                                 24.8.2.1-1                                amd64        Math module for LibreOffice 24.8.2.1
ii  libobasis24.8-ogltrans                             24.8.2.1-1                                amd64        OpenGL slide transitions module for LibreOffice 24.8.2.1
ii  libobasis24.8-onlineupdate                         24.8.2.1-1                                amd64        Online update module for LibreOffice 24.8.2.1
ii  libobasis24.8-ooofonts                             24.8.2.1-1                                amd64        3rd party free fonts for LibreOffice 24.8.2.1
ii  libobasis24.8-ooolinguistic                        24.8.2.1-1                                amd64        Linguistic module for LibreOffice 24.8.2.1
ii  libobasis24.8-postgresql-sdbc                      24.8.2.1-1                                amd64        PostgreSQL Connector driver for LibreOffice 24.8.2.1
ii  libobasis24.8-python-script-provider               24.8.2.1-1                                amd64        Script provider for Python for LibreOffice 24.8.2.1
ii  libobasis24.8-pyuno                                24.8.2.1-1                                amd64        Pyuno module for LibreOffice 24.8.2.1
ii  libobasis24.8-writer                               24.8.2.1-1                                amd64        Writer module for LibreOffice 24.8.2.1
ii  libobasis24.8-xsltfilter                           24.8.2.1-1                                amd64        XSLT filter samples module for LibreOffice 24.8.2.1
ii  libreoffice24.8                                    24.8.2.1-1                                amd64        Brand module for LibreOffice 24.8.2.1
ii  libreoffice24.8-base                               24.8.2.1-1                                amd64        Base brand module for LibreOffice 24.8.2.1
ii  libreoffice24.8-calc                               24.8.2.1-1                                amd64        Calc brand module for LibreOffice 24.8.2.1
ii  libreoffice24.8-debian-menus                       24.8.2-1                                  all          LibreOffice 24.8 desktop integration
ii  libreoffice24.8-dict-en                            24.8.2.1-1                                amd64        English dictionary for LibreOffice 24.8.2.1
ii  libreoffice24.8-dict-es                            24.8.2.1-1                                amd64        Spanish dictionary for LibreOffice 24.8.2.1
ii  libreoffice24.8-dict-fr                            24.8.2.1-1                                amd64        French dictionary for LibreOffice 24.8.2.1
ii  libreoffice24.8-draw                               24.8.2.1-1                                amd64        Draw brand module for LibreOffice 24.8.2.1
ii  libreoffice24.8-en-us                              24.8.2.1-1                                amd64        Brand language module for LibreOffice 24.8.2.1
ii  libreoffice24.8-es                                 24.8.2.1-1                                amd64        Brand language module for LibreOffice 24.8.2.1
ii  libreoffice24.8-impress                            24.8.2.1-1                                amd64        Impress brand module for LibreOffice 24.8.2.1
ii  libreoffice24.8-math                               24.8.2.1-1                                amd64        Math brand module for LibreOffice 24.8.2.1
ii  libreoffice24.8-ure                                24.8.2.1-1                                amd64        UNO Runtime Environment.2.1
ii  libreoffice24.8-writer                             24.8.2.1-1                                amd64        Writer brand module for LibreOffice 24.8.2.1
ii  libx2go-config-perl                                4.1.0.6-0x2go1+git20230818.1994+12.main.1 all          Perl X2Go::Config package
ii  libx2go-log-perl                                   4.1.0.6-0x2go1+git20230818.1994+12.main.1 all          Perl X2Go::Log package
ii  libx2go-server-db-perl                             4.1.0.6-0x2go1+git20230818.1994+12.main.1 amd64        Perl X2Go::Server::DB package
ii  libx2go-server-perl                                4.1.0.6-0x2go1+git20230818.1994+12.main.1 all          Perl X2Go::Server package
ii  libx2go-utils-perl                                 4.1.0.6-0x2go1+git20230818.1994+12.main.1 all          Perl X2Go::Utils package
ii  x2go-keyring                                       2019.08.20+git20230921.118+12.main.1      all          GnuPG keys of all X2Go developers and the X2Go archive
ii  x2goserver                                         4.1.0.6-0x2go1+git20230818.1994+12.main.1 amd64        X2Go server
ii  x2goserver-common                                  4.1.0.6-0x2go1+git20230818.1994+12.main.1 amd64        X2Go Server (common files)
ii  x2goserver-x2goagent                               4.1.0.6-0x2go1+git20230818.1994+12.main.1 amd64        X2Go Server's X2Go Agent Xserver
ii  x2goserver-x2gokdrive                              4.1.0.6-0x2go1+git20230818.1994+12.main.1 amd64        X2Go Server's X2Go KDrive Xserver
ii  x2goserver-xsession                                4.1.0.6-0x2go1+git20230818.1994+12.main.1 all          X2Go Server (Xsession runner)
ii  xserver-x2gokdrive                                 0.0.0.3-0x2go1+git20240314.283+12.main.1  amd64        KDrive graphical server backend for X2Go Server
Setting languaje --------------------------------------------

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
Disabling ldm -----------------------------------------------
Unmounting /dev/vdb -----------------------------------------
END of the road!! keep up the good work ---------------------



