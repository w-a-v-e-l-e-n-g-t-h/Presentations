# DC919  |  March 2019  |  IDS/IPS Intro Lab Exercises
Author: wavelength  ( @\_\_wavelength\_\_ )

## Introduction
These exercises are meant only as brief introductions to the tools and interfaces available in Security Onion.\

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
4. Minimize the terminal window and double-click the "Squil" icon on the desktop.   Login to Squil using the credentials that you setup when you built the Security Onion VM; note that these are not the same credentials you use to login to the system.  A new window will appear asking which networks to monitor.   There should be two options - seconion-ossec and seconion-enxxxx.   Ignore the interface labelled "ossec"; make note of what follows the hyphen on the other interface.   It should be something something similar to enp#s#, where the #-signs are numbers.  This is the name of the capture Ethernet interface used for monitoring and it will be needed later.   Click "Select All" once you have noted the Ethernet interface name and then "Start SGUIL."  The sguil interface should appear.   Make sure that the "RealTime Events" tab is selected and the box under the tab is is clear of events.   If there are events listed, click one and press F8 to clear it.   If there are more than one, keep pressing F8 until they are all cleared.
5. Bring the terminal back to the foreground.   At the command line, enter the following command:\
`sudo sleep 15s && sudo tcpreplay -i <Ethernet interface name> -t newdat3.log`\
For example, if the name of your capture Ethernet interface is "enp0s8", the command would be as follows:\
`sudo sleep 15s && sudo tcpreplay -i enp0s8 -M 100 -t newdat3.log`\
When you press enter, you will be prompted for the sudo password; use the password used to login to the VM.   Then switch back to the sguil screen and wait.
6. In about fifteen seconds, long enough to switch back to squil, tcpreplay will replay the newdat3.log pcap file and events will appear in squil.  There should be roughly 15 events, so let's take a look at some of them.
7. Click on the event with the Event Message of "GPL TELNET Bad Login".   This fields at the bottom of the window should populate.  If they do not, make sure that the checkboxes next to "Reverse DNS", "Enable External DNS", "Show Packet Data" and "Show Rule" are all checked.
8. Let's find out where this failed login attempt possibly originated from...   Next to "Whois Query" are three radio buttons; select "Src IP" and wait for the field under that to populate.  Scroll down in that field until you see "country:".  What two letter country code is present?   You can use Google to determine what country this is, or, if you scroll down to the "address:" fields, you can find it there.
9. Now that we have determined where the attack IP is likely located, we conclude that this is an unauthorized access attempt.   Squil allows you to Classify events based on the results of an investigation.   To classify this event, right-click on the "RT" on the left of the row for this event.   In the pop-up menu, go to "Update Event Status" and then chose "CAT III - Attempted Unauthorized Access (F3)".   You can also select the event and press F3.   The event will not disappear from the "RealTime Events" field.
10. The "RealTime Events" view allows you to see events as they fire in the IDS.  As a SOC analyst monitoring an IDS, this is the event queue from which you would pick and investigate events.   Now, say you want to look at all of the events that have been classified as "Attempted Unauthorized Access".   To do this, select "Query" from the squil menu bar and choose "Query by Category" and then the "CAT III: Attempted Unauthorized Access" query.  This opens a query builder screen.  With the query builder function, you can query the event catalogued by Security Onion.  For this exercise, click the "Submit" button.   A new tab with the query results will appear and the event you classified in Step 9 should be displayed.   When you are ready to continue, close this tab using the "Close" button in the upper left corner.
11. Squil also allows you to perform packet analysis in the same interface.   Select the event labelled "ET ATTACK_RESPONSE Possible /etc/passwd via SMTP (linux style)".  The fields at the bottom should populate; if they do not, make sure the checkboxes referenced in Step 7 are checked.   Using the blue color coded fields on the bottom right of the screen, we can see the header information for the packet, including source and destination IP and port.   The "DATA" field is where we want to dig for information on this attack.   According to the event description, someone attempted to email the contents of the /etc/passwd file to someone.   Using the information in the "DATA" field, examine the packet payload and determine the recipient of the file.  What is the recipient (TO:) email address?
  
### Exercise 2 - Intro to squert
1. Minimize the squil interface and open the squert interface by using the icon on the desktop.   The login is the same username and password as squil.   Once logged in, clear all of the alerts in the squert interface.   This is done by clicking on the red square next to an event and then clicking the "No Action Req'd" option on the left side of the window under "Classification".   The classification section of interface will be explained shortly.
2. Go back to your terminal once all of the events are cleared in squert. Change directory to '/opt/examples' by typing 'cd /opt/examples'.  Run tcpreplay, as shown in Exercise 1, and import bredolab-sample.pcap.\
 `sudo tcpreplay -i <Ethernet interface name> -M 100 -t bredolab.pcap`\
 You will probably be prompted for your sude password, as in Exercise 1; again, this is the same password you used to login to the VM.
3. Once tcpreplay completes, in squert, click the interface refresh button at the top of the screen.  It will be two arrows making a circle and may be marked with a red exclamation point.   After clicking this icon, at least six alerts should appear in the squert interface.
4. Click the alert marked "ET Trojan Tibs/Harnig Downloaded Activity".   Note the information that appears - the IDPS signature, including some links to information and event specific information, such as time, source host and destination host.
5. Under "Categorize 4 Event(s)", click the red square with the number four in it.  The number indicates the number of times something, in this case packets, triggered this alert.   Additional rows will appear for each of the captured packets and their capture times.   Click the event ID for any one of the packets.   This will initiate a pivot from squert to the capME! interface.   Here you will be able to examine the contains of the captured packet and, if desired, download the PCAP from the system of offline analysis.
6. Using the information presented in the capME! interface, what was the domain from which this Trojan was downloaded?  Hint: Look at the lines marked "SRC".
7. Using the information presented in the capME! interface, it appears that the webserver sent something back - what?  Hint: Look at the lines marked "DST".
8. It looks like this might be malicious.  We have the ability to classify events in squert.   Close the capME! tab and go back to the squert interface.   The event for "ET Trojan Tibs/Harnig Downloaded Activity" should still be selected.   Make sure "Categorize 4 Event(s)" is still displayed and then click the link on the left labelled "malicious" under "Classification".   If "Categorize 4 Event(s)" instead says "Categorize 0 Event(s)" or another number, click the checkbox under the red square with four in it until "Categorize 4 Event(s)" is displayed and click the "malicious" category link.
9. The event we were just looking at now will disappear from the queue.    To view it again, click the number four next to malicious in the "Classification" section.    To view the queue again after trying this, click the "YES" next to "Filtered By Object" near the top right right of the interface.   Doing this will display all of the events in the system, including categorized events.   Click the "OFF" next to "queue only" and then the "refresh" button will restore the queue.

### Exercise 3

### Exercise 4

### Exercise 5
