verzweiflung
---------
verzweiflung is a proof of concept lossy link TCP hack for Linux.  
For an explanation and the story behind it, see: https://eliasoenal.com/2017/11/10/verzweiflung-a-story-about-how-i-hacked-the-internet/

usage
---------
```
# ./verzweiflung -h
verzweiflung v0.1
Written and placed into the public domain by
Elias Oenal <verzweiflung@eliasoenal.com>

WARNING: verzweiflung violates internet standards
         don't use it in production environments

verzweiflung is a hack to fortify TCP connections against
packet loss under unreliable network conditions. Enabling
verzweiflung does not solve the underlying network issues,
but instead compounds the overall load, while shifting
the symptoms over to other users. It is a desperate tool
for desperate times - use with caution.

usage: verzweiflung [-options]
 -c             cease operation - disable verzweiflung
 -d port        destination port
 -f             force apply - no questions asked
 -g gateway     gateway (e.g. 192.168.0.1) - overrides autodetection
 -h             print this help
 -i interface   network interface (e.g. eth0) - overrides autodetection
 -l level       level of despair - the number of retransmissions
                higher values increase overhead and redundancy,
                valid values are 2 to 4
 -m             print traffic statistics
 -s port        source port
```

SSH example
---------
Server side:
```
# ./verzweiflung -s 22
protocol: 		TCP/IP
source port(s): 	22
destination port(s): 	all
retransmissions: 	3

verzweiflung: detecting network configuration...
interface:		eth0
gateway:		12.34.56.78
is the network configuration correct? (y/N) y

verzweiflung: verified network configuration.
verzweiflung: hack is inactive!
verzweiflung: setting up iptables... success
verzweiflung: setting up traffic control... success
verzweiflung: hack is active!
```
Client side:
```
# ./verzweiflung -d 22
protocol: 		TCP/IP
source port(s): 	all
destination port(s): 	22
retransmissions: 	3

verzweiflung: detecting network configuration...
interface:		enp2s0
gateway:		192.168.0.1
is the network configuration correct? (y/N) y

verzweiflung: verified network configuration.
verzweiflung: hack is inactive!
verzweiflung: setting up iptables... success
verzweiflung: setting up traffic control... success
verzweiflung: hack is active!
```