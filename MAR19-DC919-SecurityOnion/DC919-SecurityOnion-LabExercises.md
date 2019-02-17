# DC919  |  March 2019  |  IDS/IPS Intro Lab Exercises
Author: wavelength  ( @\_\_wavelength\_\_ )

## Introduction
Placeholder

## Pre-requisites
```sh
You should have a Security Onion VM completely setup to proceed.   Ideally, you would have a snapshot of the fresh install that you can revert to between exercises.\

You should have some familiarity with Linux to be able to complete these exercises.   Some step-by-step instructions are provided to familiarize you with Security Onion or to ensure that exercises work as intended.
```

## Downloads
The following files should be downloaded to your Security Onion:\
https://github.com/wave-length/Presentations/raw/master/MAR19-DC919-SecurityOnion/Files/Ex1-honeynet.org-Scan19.tar.gz

### Exercise 1
1. Once you have logged into your VM, open a terminal window by clicking on "Applications", then "Utilities" and scroll down to and click "Terminal".   Change directory to where you have stored the downloaded Exercise pcaps.   If you used the Chromium web browser, those files are stored in the "Downloads" directory.
2. Extract the files contained in Ex1-honeynet.org-Scan19.tar.gz by using the following command:\
  `mkdir ./Exercise1/ && tar fvxz Ex1-honeynet.org-Scan19.tar.gz --directory ./Exercise1`
3. Change directory into the "Exercise1" directory.
4. Minimize the terminal window and double-click the "Squil" icon on the desktop.   Login to Squil using the credentials that you setup when you built the Security Onion VM.  A new window will appear asking which networks to monitoring.   There should be two options - seconion-ossec and seconion-enxxxx.   Ignore the interface labelled "ossec"; make note of what follows the hyphen on the other interface.   It should be something something similar to enp#s#, where the #-signs are numbers.  This is the name of the Ethernet interface used for monitoring and it will be needed later.   Click "Select All" once you have noted the Ethernet interface name and then "Start SGUIL."  The sguil interface should appear.   Make sure that the "RealTime Events" tab is selected and the box under is empty of event.   If there are event listed, click one and press F8 to delete it.   If there are more than one, keep pressing F8 until they are all cleared.
5. Bring the terminal back to the foreground.   At the command line, enter the following command:\
  `sudo sleep 15s && sudo tcpreplay -i <Ethernet interface name> -t newdat3.log`
For example, if the name of your Ethernet interface is "enp0s8", the command would be as follows:\
  `sudo sleep 15s && sudo tcpreplay -i enp0s8 -t newdat3.log`
When you press enter, you will be prompted for the sudo password; use the password used to login to the VM.   Then switch back to the sguil screen and wait.
6. In about fifteen seconds, long enough to switch back to squil, tcpreplay will replay the newdat3.log pcap file and events will appear in squil.
  
### Exercise 2

### Exercise 3

### Exercise 4

### Exercise 5
