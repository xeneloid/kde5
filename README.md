## Ports for constructing the 'kde5' and 'kde5-extra' collections

Contributions are welcome. If you don't know what it all about, please take the time to read the documentation at
http://www.nutyx.org/en/build-package.html
(version française)
http://www.nutyx.org/fr/build-package.html

It will explain you what's a collection, a git, a port, the tools around 'cards' etc

### How to test this git:

#### 1. Clone it in your home directory

    $ cd
    $ git clone git://github.com/NuTyX/kde5.git
    $ git clone git://github.com/NuTyX/core.git

#### 2. Become root until the end, define and create the directory used by the scripts:

 The script is checking the files /etc/install-nutyx.conf and /etc/install-nutyx.conf.d/cards.conf if they exist, if yes it will use them, so:

    $ su -
    # echo "LFS=/mnt/lfs
    VERSION=current
    DEPOT=/DEPOT" > /etc/install-nutyx.conf
    # mkdir -p /etc/install-nutyx.conf.d
    # cat > /etc/install-nutyx.conf.d/cards.conf << "EOF"
    dir /DEPOT/kde5-extra
    dir /DEPOT/kde5
    dir /DEPOT/gui
    dir /DEPOT/cli
    dir /DEPOT/base|http://downloads.nutyx.org
    dir /DEPOT/base-extra|http://downloads.nutyx.org
    base /DEPOT/base
    base /DEPOT/base-extra
    logdir /var/log/pkgbuild
    EOF

#### 3. Install a base NuTyX system (assume below the user is 'tnut' so adapt to yours)

    # bash /home/tnut/core/scripts/install-nutyx

#### 4. In your chroot Make the directory where the git copy will comes

    # mkdir -v /mnt/lfs/root/{core,kde5}

#### 5. Mount your git project (assume below the user is 'tnut' so adapt to yours)

    # mount -o bind /home/tnut/kde5 /mnt/lfs/root/kde5
    # mount -o bind /home/tnut/core /mnt/lfs/root/core

#### 6. Enter now in your chroot

    # bash /home/tnut/core/scripts/install-nutyx -ec

#### 7. Prepare the first execution of the build script

    # get cards.devel git
 
#### 8. If everything is OK, synchronize the  core 'base', 'cli' and 'gui' collections binaries

    # cd /root/core
    # bash scripts/base -s
    # bash scripts/cli -s
    # bash scripts/gui -s
    
#### 9. If everything is OK, synchronize the 'kde5' collection binaries 

    # cd /root/kde5
    # bash scripts/kde5 -s

#### 10. If everything is OK, check with cards level what's new

    # cards level

 It should shows all the packages available.

#### 11. If you want to build the 'kde5' collection from the sources:

    # bash scripts/kde5 -a

#### 12. If you want to build the 'kde5-extra' collection from the sources:

    # cd /root/kde5
    # bash scripts/kde5-extra -s
    # bash scripts/kde5-extra -a 

Have fun :)
