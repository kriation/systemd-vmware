A few months ago, I decided to switch Linux distributions from Ubuntu to ArchLinux and have been very pleased with the experience so far. Recently, the folks at Arch decided to switch from using initscripts and sysvinit during the boot process to systemd. Systemd provides an incredibly powerful interface to service management, and I can see why the switch was made. It looks like other distributions may be switching in the near future as well.
 
While in the process of switching, I realized that I was going to have trouble with the vmware service script. My options were to run my rig in a hybrid mode, or convert the script to support systemd. I chose the latter, and the attached tarball is the result. I've tested the services on two ArchLinux instances, and they work without issue. I realize that a chunk of error checking that was in the original service script doesn't exist, but I intend to add it, as well as an overall script to kick off the sub-scripts. For now, the attached tarball includes the following service files:
 
* vmware-vmmon.service  (Virtual machine monitor)
* vmware-vmci.service (Virtual machine communication interface)
* vmware-vmsock.service (VMCI Socket Family)
* vmware-vmnet.service (Virtual ethernet)
* vmware-vmblock.service (Blocking file system)
* vmware-authentication.service (Authentication Daemon)
* vmware-usb.service (USB Arbitration Service)
 
The order in which they are started is above, with vmmon starting first, and ending with the USB Arbitration service. Any of these can be enabled/disabled based on your requirement.
 
As I mentioned above, the items left to integrate into these scripts are:
* Error condition checking when loading modules
* Checking for Shared Memory
* Implementing a single service that kicks off each of the sub-services.
