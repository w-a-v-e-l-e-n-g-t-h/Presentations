# System Requirements
```sh
CPU: minimum 4x vCPUs
RAM: minimum 8GB
HDD: minimum 40GB
```

## Downloads

Download the Security Onion ISO from the following location:
https://github.com/Security-Onion-Solutions/security-onion/releases/tag/v16.04.5.5_20181212


## VM configuration (VirtualBox)

  1.  Create a new VM using Expert Mode.   Name it whatever you would like.   Set the type to "Linux" and the version to "Ubuntu (64-bit)".
  2.  Set the memory size for the VM to a minimum of 8GB, but if possible, give the VM as much memory as you can.
  3.  Select "Create a new virtual hard disk now" and click "Create."
  4.  The virtual hard drive creation dialog screen will appear.   Specify the size of the hard drive for the VM and click "Create".
  5.  The VM should now be in the list of configured VMs.    
  6.  Right click on the VM and select "Settings".
  7.  Click on "System" and then "Processor".   Set the number vCPUs for the VM to a minimum of four, but preferrably more.
  8.  Click on "Storage" and click on the CD-ROM/DVD icon with "Empty" displayed next to it.    The menu will update and under "Attributes", "Optical Drive" will appear.   Click the CD-ROM/DVD icon in that section and select "Choose Virtual Optical Disc Format".  Go to the location where you saved the ISO file and select it.
  9.  Click on "Audio" and disable audio featurs by unchecking "Enable Audio".
  10. Click on "Network" and verify that "Adapter 1" is enabled and is attached to NAT.   Select "Adapter 2", enable it and set the "Attached to:" option to "Host-only Adapter". 
  11. Click OK.
  
 ## Setting up Security Onion VM
 
