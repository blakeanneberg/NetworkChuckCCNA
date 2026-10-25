# Cisco IOS CLI Reference & Switch Setup Guide

## Cisco IOS CLI Modes

### User EXEC Mode (`>`)
- Press `Enter` at the initial prompt to access User EXEC mode.
- Context-sensitive help: Type `?` (e.g., `?` or `ping ?`) to display syntax, commands, and parameter options.

### Privileged EXEC Mode (`#`)
- `enable`: Transitions from User EXEC mode (`>`) into Privileged EXEC mode (`#`).
- `enable secret <password>`: Sets an MD5/SHA-hashed password required to enter Privileged EXEC mode.
- Verification procedure: Enter `end`, run `disable` to drop back to User EXEC mode, then run `enable` to confirm authentication triggers.
- `reload`: Reboots the switch (does not clear saved configurations).

### Global Configuration Mode (`(config)#`)
- `configure terminal` (or `conf t`): Enters Global Configuration mode to modify system-wide parameters, interface settings, and protocols.
- `hostname <name>`: Sets or updates the device hostname.
- `banner motd #<message>#`: Sets the Message of the Day banner displayed before login prompts.
- `password <plaintext>`: Configures an unencrypted password (avoid using where hashed secrets are supported).
- `enable secret <password>`: Sets a cryptographically hashed administrative password.
- `service password-encryption`: Encrypts cleartext passwords stored in the configuration file (Type 7).
- `no <command>`: Negates a command or restores its default parameter.
- `line vty 0 4`: Configures Virtual Terminal lines for remote management access (Telnet / SSH).
- `end` (or `Ctrl + Z`): Exits directly back to Privileged EXEC mode (`#`).
- `copy running-config startup-config` (or `write memory` / `wr`): Commits active configuration changes to NVRAM.
- Factory reset procedure:
  ```cisco
  erase startup-config
  ! -- Alternative: write erase --
  delete flash:config.text
  reload
  ```
- Comparing active configuration against NVRAM:
  ```cisco
  show running-config
  show startup-config
  ```

### Interface Configuration Mode (`(config-if)#`)
- `interface <type> <slot/port>`: Enters interface configuration mode (e.g., `interface fastEthernet 0/1` or `interface gigabitEthernet 1/0/1`).
- Interface numbering syntax: Represents `module/port` (or `switch/slot/port` on stacked switches).
- `description <text>`: Attaches an administrative label or circuit identifier to the port (e.g., `description Uplink to Core`).
- `shutdown`: Administratively disables the port (Layer 1 down).
- `no shutdown`: Enables the port.
- `interface vlan 1`: Enters the Switch Virtual Interface (SVI) used for Layer 3 switch management.

---

## CLI Navigation & Shortcuts

- `exit`: Moves back one configuration level.
- `end` or `Ctrl + Z`: Jumps immediately to Privileged EXEC mode from any sub-configuration mode.
- `Up Arrow` / `Down Arrow`: Scrolls backward and forward through previous command history.
- `Tab`: Autocompletes partially typed commands or arguments.
- `do <command>`: Executes Privileged EXEC commands (such as `show` or `ping`) from within any configuration mode (e.g., `do show running-config`).

---

## Verification & Troubleshooting Commands

- `show running-config` (or `show run`): Displays the current running configuration loaded in RAM.
- `show running-config | include <string>`: Filters the configuration output for specific matching strings (e.g., `do show running-config | include hostname`).
- `show running-config | section <string>`: Displays entire hierarchical configuration blocks matching the search term (e.g., `do show running-config | section line con`).
- `show ip interface brief`: Displays a concise summary of all interfaces, assigned IP addresses, and Layer 1/Layer 2 operational statuses (`Status` / `Protocol`).
- `show interfaces status`: Displays port duplex, speed, VLAN membership, and physical link state.
- `show interfaces description`: Lists interface operational states alongside their configured descriptions.
- `show mac address-table` where a switch learns which MAC address lives on which port

---

## Base Switch Configuration Template

```cisco
enable
configure terminal

! -- Hostname --
hostname DS-07-SW1

! -- Banner --
banner motd #Castle Rysen Ops: Authorized engineers only.#

! -- Security & Passwords --
enable secret CrC0ffee!
service password-encryption

! -- Console Port Security --
line console 0
 password VaultAccess
 login
exit

! -- Remote Management Lines (VTY 0-4) --
line vty 0 4
 password ShelterAccess
 login
exit

! -- Management SVI --
interface vlan 1
 ip address 192.168.10.11 255.255.255.0
 no shutdown
exit

! -- Uplink Ports Configuration --
interface range ethernet 0/0 - 1
 description ## Uplink to DS-07-SW2 ##
exit

! -- Save Configuration --
end
write memory
```

---

## Quick Reference Command Mapping

| Task | Command Syntax |
|---|---|
| Set hostname | `hostname <name>` |
| Set login banner | `banner motd #<text>#` |
| Set enable secret | `enable secret <password>` |
| Encrypt plaintext passwords | `service password-encryption` |
| Set console password | `line console 0` $\to$ `password <pw>` $\to$ `login` |
| Set VTY password | `line vty 0 4` $\to$ `password <pw>` $\to$ `login` |
| Assign management IP on a switch | `interface vlan 1` $\to$ `ip address <ip> <mask>` $\to$ `no shutdown` |
| Add an interface description | `interface <id>` $\to$ `description <text>` |
| View all interface IPs and status | `show ip interface brief` |
| View port up/down & VLAN status | `show interfaces status` |
| View interface descriptions | `show interfaces description` |
| View running configuration | `show running-config` |
| View saved startup configuration | `show startup-config` |
| Save configuration to NVRAM | `write memory` (or `copy run start`) |
| Reload / reboot device | `reload` |
