## Version 2 has been released!
After a few years of customer feedback and development, we are happy to release a new major revision with more features, better reliability, and better scalability. See Downloads for details!


## Description:
Client to Server Traffic (ctsTraffic) was developed by members of the **Microsoft (R) Windows (R) Networking test team**. It was initially designed at the end of Windows 7 and has been used to measure networking scenarios throughout Windows 8 and Windows Blue.  We are now excited to be bringing this tooling to the open source community.

It is a utility to generate and validate the integrity of network traffic. It is a highly scalable client / server application with the ability to send and receive traffic in a variety of protocol patterns, utilizing a variety of API calling patterns. The protocol is validated in bytes sent and received for every connection established. Should there be any API failure, any connection lost prematurely, or any protocol failure in bytes sent or received, the tool will capture and log that error information. 

ctsTraffic has been tested to scale down to small devices, scale up to large systems (effectively spanning across large #s of processors; large memory installations including multiple NUMA nodes; easily filling large network pipes including 10Gig and 40Gig connections), and scaling out to large numbers of simultaneous connections (tested up to 500,000 active TCP connections).

Information about the network traffic can be captured within an Excel-friendly format to facilitate graphing interesting properties of the network session; properties such as TCP bytes/second or UDP bits/second; UDP frames processed over time; UDP frames dropped over time; connection rates successfully established over time; failed connections over time.

## Supported Features:
* Servers service any number of connections from any number of clients
* Allows for specifying the number of connections to maintain from the client
* Allows targeting one or more servers by name or address
* Allows binding or listening to specific addresses or ranges (e.g. only IPv6 addresses)
* Allows for selecting the degree to which ctsTraffic should validate the TCP session (connection integrity or additionally data integrity) 
* TCP-specific
	* Allows for specifying the buffer sizes used in send & receive calls - including specifying a range to randomly select a buffer size
	* Allows for selecting from different Winsock API usage patterns
	* Allows for selecting from various TCP protocol patterns controlling send and receive patterns
	* Allows for throttling TCP connections to send at a specified rate
* UDP-specific
	* Allows for controlling the bits/second being streamed from the server, processed on the client
	* Allows for controlling the frame to process the incoming stream
	* Allows for controlling the amount of buffering on the client before starting to process the stream
	* Allows for controlling how hard the client will work in looking ahead and requesting missing frames
* Various logging options, including toggling whether to log to console
	* Text formatting or Csv formatting
	* Per connection details; error details; aggregate status details; UDP jitter details
	* Various logging options and verbosity, allowing greater levels of detail when required
	* Various scenario-specific options for customized environments

## Setup Instructions:
Select the Downloads tab above. Copy ctsTraffic.exe to the client and server (no installation required - only a single binary).

## Usage:
_Server-side usage_
{{ ctsTraffic -Listen:<addr or *> [-Port:####](-Port_####) [CommonOptions](CommonOptions) 
}}

_Client-side usage_
{{ ctsTraffic -Target:<addr or name> [-Port:####](-Port_####) [-Connections:<####>](-Connections__####_) [-Iterations:<####>](-Iterations__####_) [CommonOptions](CommonOptions) 
}}

An example of push-pulling data between a client & server across 100 concurrent connections (to be executed across 10 iterations -> therefore 100 x 10 == 1000 total connections before exiting).

_Server_
{{ ctsTraffic.exe -Listen:* -Port:4444 -Pattern:pushpull 
}}

_Client_
{{ ctsTraffic.exe -Target:<server> -Port:4444 -Connections:100 -Iterations:10 -Pattern:pushpull 
}}


## Traffic visualization:

#### TCP Traffic visualization:
ctsTraffic allows the user to view (or log to raw text or Excel-friendly csv) TCP sessions at a specified time frequency with the following format:

_Legend_
_TimeSlice_: (seconds) cumulative runtime
_Send & Recv Rates_: bytes/sec that were transferred within the TimeSlice period
_In-Flight_: count of established connections transmitting IO pattern data
_Completed_: cumulative count of successfully completed IO patterns
_Network Errors_: cumulative count of failed IO patterns due to Winsock errors
_Data Errors_: cumulative count of failed IO patterns due to data errors

|| TimeSlice || SendBps || RecvBps || In-Flight || Completed || NetError || DataError ||
| 1.0 | 1292704 | 1280572 | 1 | 0 | 0 | 0 |
| 2.0 | 1263080 | 1286975 | 1 | 0 | 0 | 0 |
| 3.0 | 1299168 | 1286975 | 1 | 0 | 0 | 0 |
| 4.0 | 1263080 | 1286975 | 1 | 0 | 0 | 0 |
| 5.0 | 1299168 | 1286975 | 1 | 0 | 0 | 0 |
| 6.0 | 1406025 | 1285689 | 1 | 0 | 0 | 0 |
| 7.0 | 1154816 | 1389933 | 1 | 0 | 0 | 0 |
| 8.0 | 1263080 | 1132538 | 1 | 0 | 0 | 0 |
| 9.0 | 1406025 | 1439972 | 1 | 0 | 0 | 0 |
|10.0 | 1299168 | 1286975 | 1 | 0 | 0 | 0 |


#### UDP Traffic visualization
ctsTraffic allows the user to view (or log to raw text or Excel-friendly csv) UDP sessions at a specified time frequency with the following format:

_Legend_
_TimeSlice_: (seconds) cumulative runtime
_Bits/Sec_: bits streamed within the TimeSlice period
_Completed Frames_: count of frames successfully processed within the TimeSlice
_Repeated Frames_: count of frames received multiple times within the TimeSlice
_Attempted Retries_: count of retries for missing frames within the TimeSlice
_Stream Errors_: count of invalid frames or buffers within the TimeSlice

|| TimeSlice || Bits/Sec || Completed || Dropped || Repeated || Retries || Errors ||
| 5.0 | 322480601 | 302845985 | 100 | 0 | 0 | 0 |
| 10.0 | 322228495 | 321991090 | 100 | 0 | 0 | 0 |
| 15.0 | 323469312 | 322750752 | 100 | 0 | 0 | 0 |
| 20.0 | 321824358 | 322043114 | 100 | 0 | 0 | 0 |
| 25.0 | 317864670 | 317394570 | 100 | 0 | 0 | 0 |
| 30.0 | 325481267 | 325794944 | 100 | 0 | 0 | 0 |
| 35.0 | 318986649 | 318903289 | 100 | 0 | 0 | 0 |
| 40.0 | 321614643 | 321634304 | 100 | 0 | 0 | 0 |
| 45.0 | 313759660 | 314113776 | 100 | 0 | 0 | 0 |
| 50.0 | 325671321 | 325474524 | 100 | 0 | 0 | 0 |