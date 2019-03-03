# DC919  |  March 2019  |  IDS/IPS Intro Lab Exercises
Author: wavelength  ( @\_\_wavelength\_\_ )

## Introduction
These exercises are meant only as brief introductions to the tools and interfaces available in Security Onion.\
For example, Kibana is a complex and powerful tool and would require an entire class to thoroughly introduce.

## Pre-requisites
You should have a Security Onion VM completely setup to proceed.\
Ideally, you would have a snapshot of the fresh install that you can revert to between exercises.\

You should have some familiarity with Linux to be able to complete these exercises.\
Some step-by-step instructions are provided to familiarize you with Security Onion or to ensure that exercises work as intended.

## Downloads
The following files should be downloaded to your Security Onion:\
https://github.com/wave-length/Presentations/raw/master/MAR19-DC919-SecurityOnion/Files/Ex1-honeynet.org-Scan19.tar.gz

### Exercise 1 - Intro to squil
1. Once you have logged into your VM, open a terminal window by clicking on "Applications", then "Utilities" and scroll down to and click "Terminal".   Change directory to where you have stored the downloaded Exercise pcaps.   If you used the Chromium web browser, those files are stored in the "Downloads" directory.
2. Extract the files contained in Ex1-honeynet.org-Scan19.tar.gz by using the following command:\
  `mkdir ./Exercise1/ && tar fvxz Ex1-honeynet.org-Scan19.tar.gz --directory ./Exercise1`
3. Change directory into the "Exercise1" directory.
4. Minimize the terminal window and double-click the "Squil" icon on the desktop.   Login to Squil using the credentials that you setup when you built the Security Onion VM.  A new window will appear asking which networks to monitoring.   There should be two options - seconion-ossec and seconion-enxxxx.   Ignore the interface labelled "ossec"; make note of what follows the hyphen on the other interface.   It should be something something similar to enp#s#, where the #-signs are numbers.  This is the name of the Ethernet interface used for monitoring and it will be needed later.   Click "Select All" once you have noted the Ethernet interface name and then "Start SGUIL."  The sguil interface should appear.   Make sure that the "RealTime Events" tab is selected and the box under is empty of event.   If there are event listed, click one and press F8 to delete it.   If there are more than one, keep pressing F8 until they are all cleared.
5. Bring the terminal back to the foreground.   At the command line, enter the following command:\
`sudo sleep 15s && sudo tcpreplay -i <Ethernet interface name> -t newdat3.log`\
For example, if the name of your Ethernet interface is "enp0s8", the command would be as follows:\
`sudo sleep 15s && sudo tcpreplay -i enp0s8 -M 100 -t newdat3.log`\
When you press enter, you will be prompted for the sudo password; use the password used to login to the VM.   Then switch back to the sguil screen and wait.
6. In about fifteen seconds, long enough to switch back to squil, tcpreplay will replay the newdat3.log pcap file and events will appear in squil.
  
### Exercise 2 - Intro to squert
1. Minimize the squil interface and open the squert interface by using the icon on the desktop.   The login is the same username and password as squil.   Once logged in, clear all of the alerts in the squert interface.   This is done by clicking on the red square next to an event and then clicking the "No Action Req'd" option on the left side of the window.   This section of interface will be explained shortly.
2. Go back to your terminal once all of the events are cleared in squert. Change directory to '/opt/examples' by typing 'cd /opt/examples'.  Run tcpreplay, as shown in Exercise 1, and import bredolab-sample.pcap.\
 `sudo tcpreplay -i <Ethernet interface name> -M 100 -t bredolab.pcap`\
 You will probably be prompted for your root password, as in Exercise 1.
3. Once tcpreplay completes, in squert, click the interface refresh button at the top of the screen.  It will be two arrows making a circle and will likely be marked with a red exclamation point.   After clicking this icon, at least six alerts should appear in the squert interface.
4. Click the alert marked "ET Trojan Tibs/Harnig Downloaded Activity".   Note the information that appears - the IDPS signature, including some links to information and event specific information, such as time, source host and destination host.
5. Under "Categorize 4 Event(s)", click the red square with the number four in it.  The number indicates the number of packets that were observed that triggered this alert.   Additional rows will appear that show the packets and their capture times.   Click the event ID for one of the packets.   This will initiate a pivot from squert to the capME! interface.   Here you will be able to examine the contains of the captured packet and, if desired, download the PCAP from the system of offline analysis.
6. Using the information presented in the capME! interface, what was the domain from which this Trojan was downloaded?  Hint: Look at the lines marked "SRC".
7. Using the information presented in the capME! interface, it appears that the webserver sent something back - what?  Hint: Look at the lines marked "DST".
8. It looks like this might be malicious.  We have the ability to classify events in squert.   Close the capME! tab and go back to the squert interface.   The event for "ET Trojan Tibs/Harnig Downloaded Activity" should still be selected.   Make sure "Categorize 4 Event(s)" is still displayed and then click the link on the left labelled "malicious" under "Classification".   If "Categorize 4 Event(s)" instead says "Categorize 0 Event(s)" or another number, click the checkbox under the red square with four in it until "Categorize 4 Event(s)" is displayed and click the "malicious" category link.
9. The event we were just looking at now will disappear from the queue.    To view it again, click the number four next to malicious in the "Classification" section.    To view the queue again after trying this, click the "YES" next to "Filtered By Object" near the top right right of the interface.   Doing this will display all of the events in the system, including categorized events.   Click the "OFF" next to "queue only" and then the "refresh" button will restore the queue.

### Exercise 3

### Exercise 4

### Exercise 5
