# Ubuntu Install
### My experience getting started with the Linux OS

## Background
I had used Windows PC's growing up and even built a custom machine about 10 years ago. However, after a few moves, this machine stayed tucked away in box and I relied solely on my 2018 Macbook Pro for the past couple of years. The Macbook Pro was more portible, easier to setup/use, and had my entire dev environment - I've been very comfortible using it. So I had experience with Windows - thinking it was just OK - and, more recently, experience with MacOS - thinking it was pretty great. As I've been getting deeper into software development though, Linux has become intriguing - admittedly, pretty much just based on it "coolness" and my sense that other developers like the opensource operating system. 

About a year ago, I had spent a few days playing around with Virtual Machines and booted up Ubuntu to explore a bit. I pretty much stuck to the Terminal and my takeaway was "ok, nice" but never drove in further after destroying the VM. Then, a few days ago I was gifted an Alienware X51 R2 machine with Windows 10 installed on it. I figured I'd trun this into my Linux machine and use it going forward to work on personal development projects. Although it is not drastically different from MacOS (both are unix based), I thought it will be benefitial to have the "developement via Linux" skills and having a "fresh" machine was exciting. I could run installations and setup a completely new dev environment - this time taking notes and taking the time to understand the nuance (previously, on my Mac, setup was a bit chaotic).

## Getting Started 
Ok, so I'v got this PC (running Windows 10) and I want a Linux-based OS to do software developement on - now what? I am slightly familiar with Windows (having used it extensivelty in the past but not recently) and dabbled with Ubuntu via a VM for a few minutes a year ago - thats about it. I knew there were different "flavors" of Linux (Ubuntu being the only one I had really heard of though) so I did a quick "best linux distrubution for software developement". I quickly had it narrowed down to either Ubuntu 20.04 LTS or Fedora 32 Workstation. I ended up going with Ubuntu because I had poked around with it in the past, the latest release was brand new, and there is lots of support / documationation around (i.e. it is very popular).

Sweet, I've got my Linux distrubution picked out (Ubuntu 20.04 LTS) - now it is time to get it installed. I had heard of the concept of "dual booting" and it made sense to me - I'll keep Windows 10 installed and then installed Ubuntu to run along side it. However, right off the bat, I felt a bit overwhelmed - this was going to be tricker than I originally anticipated. I hadnt given much though to the hardware components (due primarily to ignorance on the topic) and found myself without the recommended pieces (namely, a couple of 4GB+ USB Flash Drive). 

## Here We Go
First, it was recommended to backup Windows to a flash drive. I went digging in an old backback and found a couple of ancient USB sticks. "Awesome, these should do the trick" I thought - but, after plugging-in and inspecting them, realized they were a tiny 1GB. Won't do, we need at least 16GB. So I decided to skip this step thinking that I want to keep Windows and dual boot alongside it - we should be fine (this was my first mistake).

Next, after some exploring, it became clear that installing Ubuntu wasn't as cut & dry as I had assumed. I discovered that it requires either (another) USB drive (4GB+) or a CD/DVD. Again, I found myself lacking the required hardware. At this point, I remembered that I had a external HHD siting around in a box and decided to go dig that out in hopes of using it in place of a USB flash drive. Success! I plugged it in - plenty of space (500GB) and just a few old documents from collage on there. Next I downloaded the Ubunto ISO file along with Rufus and proceeded to install the iso on the external hard drive (within rufus tool, needed to select "Show advanced drive properties" and enable "List USB Hard Drive" option). Once complete, I rebooted and entered the BIOS menu, navigated to Boot section then A) enabled boot from USB and B) made the USB 1st boot option. After saving & rebooting, the Ubuntu demo was launched.

## Making Progress
It took me a few minutes to realize that I wasn't done quite yet - Ubuntu booted and ran but it was not installed. In other word, I could use the Ubuntu OS just fine but on reboot / shitdown all data & programs would be wiped. Conventiently, there is a "Install Ubuntu" icon placed on the desktop. Clicking this prompts the Installation Guide - this is wear I ran into trouble. I indended on installing Ubuntu onto the external harddrive itself (with intentionals of having a portable OS) but I now realize that, beacuse the boot loader was on the hard drive, this is not possible. So when I went to install, I was actually putting Ubuntu onto the PC harddrive. With this mistake / confusion, I proceeded to wipe Windows and replace it with Ubunti by selecting the "Something Else" installation type and manually setting partitions. By selecting this option, instead of the "Install Ubuntu besdides Windows 10", I wrote over Windows and eliminated ability to dual boot. Not a huge loss, luckily not much was on that disk and I wasn't planning on using that OS much. Mostly, just bummed about not having the option itself but can alway look to add Windows 10 back in the future. By the way, I came to the conclusion that I had messed-up & removed Windows after A) not seeing "Windows Boot Manager" in the Bios Boot menu and B) not seeing any partitions with a type of NTFS (executing: $ sudo fdisk -l).

Ultimately, I ended up with Ubuntu 20.04 LTS booting up and working great. Yay! First thing I did was to reformat to external hard drive (using Gpart) so I could again use it as indended (backup / data storage) and so Ubuntu would recognize it. Next up: getting my dev environment setup. Stay tuned! 

## Conclusions
 - take the time to do more research and read about entire process. step-by-step approach causes problems 
 - try to anticipdate issues ahead of time (mentally walkthrough the process, google details)
 - be patient - if dont have the proper hardware, hold off and go get it 
 - ensure going into something new, there is ability / tollerance for mistakes. if i had had valuable data on the Windows disk, it would have been bad.

## References
 - https://www.youtube.com/watch?v=sg4GOLWar44
 - https://www.youtube.com/watch?v=fGNl0KxOt7Q
 - https://www.youtube.com/watch?v=Pn7jZ5i1RTM
 - https://help.ubuntu.com/lts/installation-guide/
 - https://support.microsoft.com/en-us/help/4026852/windows-create-a-recovery-drive
 - https://help.ubuntu.com/community/GettingUbuntu
 - https://help.ubuntu.com/community/Installation/FromUSBStick
 - https://ubuntu.com/tutorials/tutorial-create-a-usb-stick-on-windows#1-overview
 - https://www.dell.com/support/article/en-us/sln301754/how-to-install-ubuntu-and-windows-8-or-10-as-a-dual-boot-on-your-dell-pc
 - https://linuxhint.com/rufus_bootable_usb_install_ubuntu_18-04_lts/
 - https://www.howtogeek.com/howto/35676/how-to-choose-a-partition-scheme-for-your-linux-pc/
 - https://askubuntu.com/questions/343268/how-to-use-manual-partitioning-during-installation
 - https://askubuntu.com/questions/987228/can-i-dual-boot-using-an-external-hard-drive

## P.S. - Some Helpful Shortcuts & Commands
 - prompt terminal:
  
<kbd>Alt</kbd>+<kbd>Ctrl</kbd>+<kbd>t</kbd>
 - copy & paste within terminal:
  
<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>c</kbd>
<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>v</kbd>
 - get machine name: 
```bash
$ sudo dmidecode | less | grep "Product Name"
```
 - view partitions:
```bash
$ sudo fdisk -l
```