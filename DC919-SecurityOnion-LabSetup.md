# DC919  |  February 2019  |  IDS/IPS Intro Lab
Author: wavelength  ( @\_\_wavelength\_\_ )

## Introduction
This guide will walk you through getting an "evaluation" Security Onion VM setup in Virtual Box (and if I have time, VMWare Player).   I am making no assumptions on your level of knowledge, so this is written so even a novice can walkthrough these instructions.

## System Requirements
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
  4.  The virtual hard drive creation dialog screen will appear.   Specify the size of the hard drive for the VM and click "Create".   The minimum size of the drive should be 40GB.
  5.  The VM should now be in the list of configured VMs.    
  6.  Right click on the VM and select "Settings".
  7.  Click on "System" and then "Processor".   Set the number vCPUs for the VM to a minimum of four, but preferrably more.
  8.  Click on "Storage" and click on the CD-ROM/DVD icon with "Empty" displayed next to it.    The menu will update and under "Attributes", "Optical Drive" will appear.   Click the CD-ROM/DVD icon in that section and select "Choose Virtual Optical Disc Format".  Go to the location where you saved the ISO file and select it.
  9.  Click on "Audio" and disable audio features by unchecking "Enable Audio".
  10. Click on "Network" and verify that "Adapter 1" is enabled and is attached to NAT.   Select "Adapter 2", enable it and set the "Attached to:" option to "Host-only Adapter". 
  11. Click OK.
  
 ## Setting up Security Onion VM
  1.  Power on the newly created VM.
  2.  When the Security Onion bootloader screen appears, choose "Boot SecurityOnion 16.04.5.5" and press enter.
  3.  The Security Onion desktop will appear.   On this screen, double click the "Install SecurityOnion 16.04" icon.
  4.  Select the language you want to use and click "Continue".
  5.  On the "Preparing to install SecurityOnion" screen, check the "Download updates while installing SecurityOnion" option and click "Continue". 
  6.  On the "Installation type", select "Erase disk and install SecurityOnion".   Click "Install Now".
  7.  A confirmation screen will appear labelled "Write the changes to disks?".   Click "Continue".
  8.  On the "Where are you?" screen, select "New York" for the Eastern time zone.   Click "Continue".
  9.  On the "Keyboard layout" screen, select your preferred keyboard layout and language.   Click "Continue".
  10. Fill out the "Who are you?" screen with your information and password.   Note - you can not use the username 'root'.   Click "Continue" when you have filled out all the required fields.
  11. The "Install" window will appear will Security Onion installs.   Wait for this process to complete.
  12. When the "Installation Complete" prompt appears, click "Restart Now".   The VM will shutdown.   When prompted, press "Enter".
  13. The system will reboot.   Allow the bootloader counter to complete and boot automatically.
  14. Login with the account you setup in step 10.
  15. Double-click the "Setup" icon on the Desktop.   You will be prompted for the password for administrative tasks.   This is the password you used to login to Security Onion. 
  16. On the "Security Onion Setup..." screen, click "Yes, Continue!".
  17. When asked if you would "like to configure /etc/network/interfaces now?", click the "Yes" option.
  18. Select the first interface in the list to be the "management interface" and click "OK".
  19. When asked to use "DHCP or static addressing", select "DHCP" and click "OK".
  20. When asked if you would "like to configure sniffing (monitor) interfaces?", click the "Yes" option.
  21. Select the remaining interface listed to be the "sniffing" interface and click "OK".
  22. Click the "Yes, make changes!" option when prompted.
  23. Click the "Yes, reboot!" option when prompted.
  24. The system will now reboot.   Allow the system to automatically boot back to the login screen.
  25. Login again.
  26. Double-click the "Setup" icon on the Desktop again.  You will be prompted for the password for administrative tasks.   This is the password you used to login to Security Onion.
  27. On the "Security Onion Setup..." screen, click "Yes, Continue!" again.
  28. When asked if you would "like to skip network configuration?", click the "Yes" option.
  29. When asked if you would like to use "Evaluation Mode or Production Mode", select "Evaluation Mode" and click "OK".
  30. When asked "which network interface should be monitoring?", make sure that the second interface (which you selected in Step 21) is still selected.   Click "OK".
  31. On the "Let's create our first user account", enter a username.   Make note of it.   This will be used to login to the Security Onion applications and is separate of the password used to login to the OS.   Click "OK".
  32. You will next be prompted for a password to be used with the account created in Step 31.   Enter a password and make note of it.   Click "OK".   Confirm the password and click "OK". 
  33. A prompt will appear listing all of the changes that the setup will make to the system.    Click the "Yes, proceed with the changes!" option.
  34. The setup process will now proceed.   Let this process run until it completes.
  35. On the "Security Onion Setup is now complete!" screen, click "OK".   Read each of the screens that appears next.  I recommend making note of the commands as they are useful to know.
  36. Once you have clicked through all of the prompts, open a terminal window by going to "Applications", "System Tools" and then "Xfce Terminal".
  37. At the command prompt, enter the following command "sudo ufw allow 443" and, if prompted for a password, enter the same password used to login to Security Onion.   Also run the command "sudo ufw allow 7443"; again, if prompted for a password, use the password used to login to Security Onion. 
  40. At this point, you can shutdown Security Onion by clicking on the icon in the upper right corner of the VM screen, then the power button icon and finally "Power Off".   
  39. (Optional) You can make a Clone of the VM if you would like to have a copy to revert to after trying out the system.
