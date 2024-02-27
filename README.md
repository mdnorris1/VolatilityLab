# Volatility

As part of the brilliant Antisyphon training with John Strand, I got to use Volatility to help analyse a memory dump of a compromised system, by looking at the network connections and process information for the malware.

After extracting Volatility, using the code: 

cd /mnt/c/IntroLabs/

tar xvfz ./volatility3-1.0.0.tar.gz

cd volatility3-1.0.0/


We used a netscan command: 


<br/>
<img src="assets/1a.png" height="80%" width="80%" alt="ifconfig command"/>
<br />

We found a computer had an established connection to another system and this was unusual.

<br/>
<img src="assets/connection.png" height="80%" width="80%" alt="ifconfig command"/>
<br />

Next, we needed to see the processes / process IDs so ran this code:

<br/>
<img src="assets/processes.png" height="80%" width="80%" alt="ifconfig command"/>
<br />

You should see the main Wireshark screen change

Then, close the Conversations window.

Notice the following in the filter bar

`ip.addr==68.183.138.51 && ip.addr==192.168.99.52`

<br/>
<img src="https://github.com/mdnorris1/WiresharkLab/blob/main/assets/css/filterbar5.png" height="80%" width="80%" alt="ifconfig command"/>
<br />

This is saying:

"IP address equals 68.183.138.51 And IP address equals 192.168.99.52"

If a packet meets both of those critiera it is displayed.

Now, right-click on any of the packets and select Follow > TCP Stream:

This is showing the request (in red) and the response (in blue) between our two systems:

<br/>
<img src="https://github.com/mdnorris1/WiresharkLab/blob/main/assets/css/request6.png" height="80%" width="80%" alt="ifconfig command"/>
<br />

There is a lot of encoded PowerShell here.

I then got to try some basic filters in the filter bar, so after filtering on IP addresses, I was now filtering on protocols.

using the filter: llmnr.

Then hit enter.

Notice that when you type llmnr and hit enter, Wireshark shows you all packets that are that protocol

Now try ipv6 and hit enter:

This allows you to very quickly drill in on any specific protocols you are reviewing in a packet capture.

<br/>
<img src="https://github.com/mdnorris1/WiresharkLab/blob/main/assets/css/ipv67.png" height="80%" width="80%" alt="ifconfig command"/>
<br />

We had previously found the string New-Object in tcpdump so now I could search though all the http traffic looking for that specific string, by putting the following into the filter bar:

http contains "New-Object"

With Wireshark, we can search through all our packets looking for specific strings and data.

<br/>
<img src="https://github.com/mdnorris1/WiresharkLab/blob/main/assets/css/newobject8.png" height="80%" width="80%" alt="ifconfig command"/>
<br />

Hope you enjoyed the walkthrough of the project!
