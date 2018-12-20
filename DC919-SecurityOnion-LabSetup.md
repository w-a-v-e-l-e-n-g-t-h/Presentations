# System Requirements
```sh
CPU: minimum 4x vCPUs
RAM: minimum 8GB
HDD: minimum 40GB
```

## VM configuration (VirtualBox)

  1.  Create a new VM using Expert Mode.   Name it whatever you would like.   Set the type to "Linux" and the version to "Ubuntu (64-bit)".
  2.  Set the memory size for the VM to a minimum of 8GB, but if possible, give the VM as much memory as you can.
  3.  Select "Create a new virtual hard disk now" and click "Create."
  4.  The virtual hard drive creation dialog screen will appear.   Specify the size of the hard drive for the VM and click "Create".
  5.  The VM should now be in the list of configured VMs.    
  6.  Right click on the VM and select "Settings".
  7.  Click on "System" and then "Processor".   Set the number vCPUs for the VM to a minimum of four, but preferrably more.
  8.  Click on "Audio" and disable audio featurs by unchecking "Enable Audio".
  9.  Click on "Network" and verify that "Adapter 1" is enabled and is attached to NAT.   Select "Adapter 2", enable it and set the "Attached to:" option to "Host-only Adapter". 
