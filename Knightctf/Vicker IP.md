We need to open the pcap file in wireshark. I wasn't sure which stream to filter out here and what exactly to look for but on reading a writeup later i saw that they 
had filtered out the http stream specifically and there were lot of requests to random files which generated 404 not found error ( bruteforce attack?) and the
ip addresses of the attacker (which requested the files) and the victim (recieved the requests) were submitted as the flag in the given flag sequence
