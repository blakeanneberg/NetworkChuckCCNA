# Cool Tips

# Backups of Cisco Switches
- `show run` and copy all commands that are shown as things that I typed, and then past it into nvim and get new switch and paste commands and thats the backup
- If switch has been running for years, dont reboot it, make sure you have backup plan if RAM is bad. Have saved copy of config, have a spare ready
- Not a chaos monkey: if switch dies, replace hardware, connect to console, restore config. 
- IF you mess up on a switch, dont save, just restart.

# MAC Addresses  
- `nmcli dev show` shows mac address on a switch
- Switches live at Layer 2 and forward traffic based on MAC addresses. layer 2 uses mac addresses inside the frames, device adds a destination MAC address and a source MAC address

# Layer 2
- FCS, or Frame Check Sequence or the CRC, or cyclical redundancy check: Same idea for both. It's a mathematical value used so the receiving device can verify the frame wasn't corrupted during transmission.
- A frame is the Layer 2 wrapper around data, including source MAC, destination MAC, and FCS.

