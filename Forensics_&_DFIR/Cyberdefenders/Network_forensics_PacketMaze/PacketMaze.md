# PacketMaze

##  The Plot

As a soc analyst working for a security service provider, you have been tasked with analyzing a packet capture for a customer's employee whose network activity has been monitored for a while -possible insider.

**SPOILER WARNING:** Since this is a retired CTF, I will be revealing the answers.

## Q1: What is the FTP password?

For this I used network miner, load the pcap-file, Check the tab called "Credentials". Look for the FTP protocol. 
````
Answer: AfricaCTF2021
````

## Q2: What is the IPv6 address of the DNS server used by 192.168.1.26? (####::####:####:####:####) answer hides in the Software registry file under: SOFTWARE\Microsoft\Windows NT\CurrentVersion. Keep in mind that information about Windows resides in the Software file because Windows OS is considered software, or at least the registry thinks so. I am using Registry Explorer for registry forensics, a great tool written by Eric Zimmerman.

Open Caploader, go to the "Hosts", check for IPv6 host having DNS port open. 
````
Answer: fe80::c80b:adff:feaa:1db7
````
## Q3: What domain is the user looking up in packet 15174?

Open wireshark --> go --> Go to the packet --> paste the packet-number (in this case 15174). --> Find the domain in the text (next to the hex value).
````
Answer: www.7-zip.org
````
## Q4: How many UDP packets were sent from 192.168.1.26 to 24.39.217.246

This was prerry straight forward. Make a query in wireshark to look for ip.src == 192.168.1.26 && ip.dst == 24.39.217.246 && ip.proto == UDP.
````
Answer: 10
````
## Q5: What is the MAC address of the system being investigated in the PCAP?

Networkminer --> Hosts --> Open the 192.168.1.26 host --> The MAC address should be there. (remember to put : after every other character/number.)
````
Answer: C8:09:A8:57:47:93
````
## Q6: What was the camera model name used to take picture 20210429_152157.jpg

Networkminer  --> Images --> find the image by name --> Open it, copy its path on your system --> Open cmd and type ""exiftool(-k).exe" C:\Users\qvist\Desktop\tools\NetworkMinerProfessional_2-8\AssembledFiles\192.168.1.20\TCP-34391\20210429_152157.jpg | grep Camera"
````
Answer: LM-Q725K
````
## Q7: What is the server certificate public key that was used in TLS session: da4a0000342e4b73459d7360b4bea971cc303ac18d29b99067e46d16cc07f4ff?

