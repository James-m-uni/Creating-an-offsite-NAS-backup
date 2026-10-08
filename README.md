# Creating an offsite network backup server for your home NAS
Having a backup of your data is important for any person - not just buisnesses.
Many people get caught out by not having a backup when they need it most even if most think
they don't need one.

You don't need fancy equipment to create your own offsite backup, even older computers will work.

For my setup I have used an older HP Compaq desktop and that is what this tutorial will be based around.

There is an easy way to connect your backup server to your home LAN without dangerous port forwarding.


## Prerequisites
For your new backup to really function as an "offsite" backup , it must be hosted in a different location
to your main backup. The main reason for this is if there is a power cut/flood etc in your main location
you still have a computer in a safe location that has a copy of your data.

Ideally have NAS on your LAN as well thus allowing for automatic backups late at night.

Your backup server must also be on all the time to allow for backups. I am also using my offsite server to host an 
Unreal engine 5 multi editor server.

This tutorial/setup makes use of tailscale ADD INFO

It is preffered to have a setup like this running through Ethernet instead of wifi as error correction through wifi will
slow down file transfer performance and occasional signal dropout may occur.

## Choice of computer + operating system
The computer you choose to run your server on depends entirely on what operations/type of software you will be using.
In the case of my home NAS, it is running on an 8gb Raspberry Pi 5 as the software im using is compatible with arm
architecture. 

<u>Positives of a raspberry pi:</u>

* Low power
* Low cost
* Small form factor so can fit into smaller spaces such as a cupboard
* Quiet

<u>Negatives of a raspberry pi</u>

* Limited number of applications that will run on the architecture

If you decide to use a raspberry pi in your project, I reccommend using the latest version or raspbian that supports the
model you choose. A later revision Raspberry PI is better suited due to having better processor performance and more memory.

For my setup, I am choosing a HP Compaq with a 3rd generation Core-i5 intel processor. This computer is running the latest version
of linux mint. I have not chosen Windows because the operating system itself uses alot of computing power even at idle which is less
ideal for older machines. This computer has been upgraded to have 16gb of memory as well.

## Storage choice
The type/size of the storage medium you choose also depends on what you are planning to use your server for along with the computer
you have chosen.

I have chosen a 2TB Seagate hard drive to be used in my HP as I wanted to have a larger amount of storage for the price. Since this computer
will mostly only be holding backups the read/write speed was less of a concern. Even if I had gone with an SSD for this, the network connection
would have become saturated long before the read/write max speed of the SSD was hit. The main operating system is stored on a 240gb SSD.

If using a sata hard drive with a raspberry PI, you will need to buy a usb to sata adapter. 3.5inch hard drives require more power
especially during start up so you will want an adapted that has its own power supply as well.

Newer Raspberry PIs support the use of NVMe through the use of a HAT.

## Network considerations
Having a stable, semi-fast internet connection is essential especially for file transfers. The network at the backup site is slower than my main internet
connection (Backup site: ~70mbps download ~16mbps upload vs Main site: ~300mbps download ~30mbps upload) however is still plenty fast enough to support this server.


# Initial setup
First we need to install the operating system. In my case, I am using <a href="https://linuxmint.com">Linux mint</a>.
The easiest way to install this is to download the iso file of the version you want. To image the file to a USB drive
so you can boot into the USB for install, you can use a tool such as <a href="https://rufus.ie/en/">Rufus</a> which allows for creation of
bootable USB images from an ISO file.

Once that is done, you can boot into your new flash drive and begin install. The key you may need to press at the BIOS will be different depending on
the computer manufacturer. In my case, I have to press the ESC key.

<b>The initial OS setup for Raspberry PI is different. You have to use the <a href="https://www.raspberrypi.com/software/">Raspberry Pi imager</a> software to put the
OS image onto an SD card to boot to.</b>


