# edr_blocker
Blocks EDR Telemetry by performing Man-in-the-Middle attack where network filtering is applied using iptables. The destination IP addresses are generated based on the server name in TLS Client Hello packet and the provided block list in a file. 

```
# python3 edr_blocker.py -h

 ______   _____    ______       ______   __       ______   ______   __  __   ______   ______
/\  ___\ /\  __-. /\  == \     /\  == \ /\ \     /\  __ \ /\  ___\ /\ \/ /  /\  ___\ /\  == \
\ \  __\ \ \ \/\ \\ \  __<     \ \  __< \ \ \____\ \ \/\ \\ \ \____\ \  _"-.\ \  __\ \ \  __<
 \ \_____\\ \____- \ \_\ \_\    \ \_____\\ \_____\\ \_____\\ \_____\\ \_\ \_\\ \_____\\ \_\ \_\
  \/_____/ \/____/  \/_/ /_/     \/_____/ \/_____/ \/_____/ \/_____/ \/_/\/_/ \/_____/ \/_/ /_/

                                                            by Tier Zero Security - New Zealand

usage: edr_blocker.py [-h] -i INTERFACE -f FILE [-m] [-v] -t TARGET -gw GATEWAY

Performs ARP Poisoning against victim host(s) and blocks EDR telemetry by utilising iptables.

options:
  -h, --help            show this help message and exit
  -i INTERFACE, --interface INTERFACE
                        Network interface to sniff on
  -f FILE, --file FILE  File containing the list of blocked server names or a part of the name 
  -m, --monitor         Monitor mode: only detect and log blocked IPs, do not add iptables rules
  -v, --verbose         Enable verbose output
  -t TARGET, --target TARGET
                        Target IP address or range (e.g., 192.168.0.1-10 or 192.168.0.1,192.168.0.2 (no space)
  -gw GATEWAY, --gateway GATEWAY
                        Gateway IP address

Example: python3 edr_blocker.py -i eth0 -f mde_block.txt -t 192.168.0.50 -gw 192.168.0.1
```

## FILE
block_mde.txt:
```
events.data.microsoft.com
wd.microsoft.com
winatp-gw-cus
automatedirstrprdcus
endpoint.security.microsoft.com
smartscreen.microsoft.com
```

block_cs.txt:
```
cloudsink.net
```
# Installing edr_blocker.py
```
git clone git@github.com:TierZeroSecurity/edr_blocker.git
cd edr_blocker
```
Install python venv
```
pip install virtualenv
```
Create virtual environment
```
python3 -m venv myenv
```
Install Python Scapy
```
source myenv/bin/activate
sudo pip install scapy
```
Run edr_blocker.py
```
sudo python3 edr_blocker.py -h
```
