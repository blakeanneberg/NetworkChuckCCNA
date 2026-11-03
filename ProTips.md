# Cool Tips

# Backups of Cisco Switches
- `show run` and copy all commands that are shown as things that I typed, and then past it into nvim and get new switch and paste commands and thats the backup
- If switch has been running for years, dont reboot it, make sure you have backup plan if RAM is bad. Have saved copy of config, have a spare ready
- Not a chaos monkey: if switch dies, replace hardware, connect to console, restore config. 
- IF you mess up on a switch, dont save, just restart.

# MAC Addresses  
- `nmcli dev show` shows mac address on a switch
- Switches live at Layer 2 and forward traffic based on MAC addresses. layer 2 uses mac addresses inside the frames, device adds a destination MAC address and a source MAC address
- ARP caches age out, so if a device isnt talking it may disapeer from the exact tables you r relying on. so just generate traffic on purpose by Ping, then check tables again. 

## Finding devices: 
1. `ping` ip address of target device
2. `show arp`
3. `show mac address-table `MAC table to find the port
4. if that port leads to another switch use `show cdp neighbors`, next switch
5. repeat till you hit the endpoint.
6. once you find the device, check interface statistics, errors, packet counts, CRC problems, to check for bad cabling, a duplex mismatch, a noisy link, or something else 


# Layer 2
- FCS, or Frame Check Sequence or the CRC, or cyclical redundancy check: Same idea for both. It's a mathematical value used so the receiving device can verify the frame wasn't corrupted during transmission.
- A frame is the Layer 2 wrapper around data, including source MAC, destination MAC, and FCS.

# ARP
- Address Resolution Protocol:  device takes an IP address and figures out the MAC address tied to it on the local network
- ARP Request: Message broadcast asking anyone a address goes to which MAC address
- Broadcasts get flooded, but known unicast traffic gets forwarded intelligently.

# STP
- Spanning Tree Protocol keeps redundant switch links from creating loops.
