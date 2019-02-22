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
`sudo sleep 15s && sudo tcpreplay -i <Ethernet interface name> -t newdat3.log`\
For example, if the name of your Ethernet interface is "enp0s8", the command would be as follows:\
`sudo sleep 15s && sudo tcpreplay -i enp0s8 -t newdat3.log`\
When you press enter, you will be prompted for the sudo password; use the password used to login to the VM.   Then switch back to the sguil screen and wait.
6. In about fifteen seconds, long enough to switch back to squil, tcpreplay will replay the newdat3.log pcap file and events will appear in squil.
  
### Exercise 2
1. If there are any alerts still present in squil, clear them before proceeding.
2. Run tcpreplay, as shown in Exercise 1, and import Ex2-RealEvent.pcap.
3. What alert did this PCAP generate?
4. What is the source IP and port of this packet?   What is the destination IP and port of this packet?
5. Research the alert using the information provided and the following links:\
\
https://attack.mitre.org/software/S0153/ \
https://blogs.jpcert.or.jp/en/2017/04/redleaves---malware-based-on-open-source-rat.html \
https://www.carbonblack.com/2017/05/09/carbon-black-threat-research-dissects-red-leaves-malware-leverages-dll-side-loading/ \
\
What is the platform (OS) that this malware affects?   What is the primary method that this malware uses to infect systems (hint: it is platform specific)?\
6. After additional investigation with your operations team, you determine that both systems in this conversation are Linux servers.   Is this malware compatible with these servers?
7. Based on the information gathered in your investigation, what would be your determination - valid alert or false positive?

### Exercise 3

### Exercise 4

### Exercise 5
