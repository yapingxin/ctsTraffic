# ctsTraffic

Forked from kehorton-zz/ctsTraffic.

Client to Server Traffic (ctsTraffic) was developed by members of the Microsoft (R) Windows (R) Networking test team.
It was initially designed at the end of Windows 7 and has been used to measure networking scenarios throughout each 
successive Windows release, including the current Windows releases.

It is a utility to generate and validate the integrity of network traffic. It is a highly scalable client / server application
with the ability to send and receive traffic in a variety of protocol patterns, utilizing a variety of API calling patterns.
The protocol is validated in bytes sent and received for every connection established. Should there be any API failure,
any connection lost prematurely, or any protocol failure in bytes sent or received, the tool will capture and log that error
information. 

ctsTraffic has been tested to scale down to small devices, scale up to large systems (effectively spanning across large #s
of processors; large memory installations including multiple NUMA nodes; easily filling large network pipes including 10Gig
and 40Gig connections), and scaling out to large numbers of simultaneous connections (tested up to 500,000 active TCP connections).

Information about the network traffic can be captured within an Excel-friendly format to facilitate graphing interesting
properties of the network session; properties such as TCP bytes/second or UDP bits/second; UDP frames processed over time;
UDP frames dropped over time; connection rates successfully established over time; failed connections over time.
