# Cisco IOS CLI Modes

## User Mode `>`
- Press enter to get in to user mode 
- `?` ex `? ping` help manual

## Privileged Mode `enable`
- `enable` goes into `#` privileged mode
- `enable secret` to allow only authenticated staff, type `end` then `disable` to drop back to user EXEC, and `enable` to re-enter privileged EXEC and re-enter password. 
- `reload` reboots the switch

### Global Configure Mode `configure` 
- `configure` to enter global configuration mode
- `hostname` to change name ef switch
- `configure terminal` or `conf t` can edit module/port interface like speed
- `banner motd` message of the day, like don't log in please.
- `password` don't use, in plain text
- `secret` use, is hash, example `secret PASSWORD`
- `service password-encryption` enables password encryption and verify by using `do show running-config | include secret`
- `no` removes a configuration
- `end` or ctl `z` gets out of Global Config mode and back to Privileged Mode
- `line vty` virtual terminal, remote into switch.
- `copy running-config startup-config`
- `reload` reboots the device but does not erase any config by itself.
- `erase startup-config` factory resets then `write erase` or `delete flash:config.text` 
- compaire running config to startup config `show startup config` and then `show running-config`


#### Interface 
- `interface fastEtherent`
- ports are module/port EX module 0 and interface 1 is 0/1
- `descrption` writes a note on the port. EX  `description "playground WAP"`
- `shutdown` turns off that module/port, `no shutdown` turns it back on
- `interface vlan 1`

## Navigation from Global Configure mode
- `Exit` takes you back one level at a time
- `End` / `CTRL + Z`
- Arrows up arrows show command history
- Tab 

### Show
#### Show Run
- `show run` shows all commands entered into the switch
- `show running config` shows hostname and interface descriptions
- ` do show running-config | include hostname` shows hostname 

#### `show IP interface brief` 
- `show run` gives verbose info for all ports 
- `show ip interface brief` shows all ports and if they are up or down

## Example Switch/Router Base Config
- `hostname`
- `banner motd #Blake Ops: Authorized engineers only.#` 
- `enable password` 
- `line console 0` blocks user mode, on the console port/line, then set a `password` then `login` and then `exit` and verify by do show running-config | section line con
- `line vty` virtual terminal, remote into switch. Example `line vty 0 4` is for ports 1 though 5
- configure management IP address via `interface vlan 1` and then `ip address 192.168.10.11 255.255.255.0` and then `no shutdown`
- `descriptions` write comment/description/note for a port via example `int fa0/1` and then `descrition` 
- `copy running-config startup-config` saves changes to base config or just write `wr`
- `do show interfaces status` idenitfy uplink ports
- identify and lable uplink and device ports `do show interfaces status` and then `interface range ethernet 0/0 - 1` and then `description ## Uplink to DS-07-SW1` and then view what you did via `do show interfaces descrption`




Set hostname	hostname <name>
Set login banner	banner motd #<text>#
Set enable secret	enable secret <password>
Encrypt plaintext passwords	service password-encryption
Set console password	line console 0 then password <pw> and login
Set VTY password	line vty 0 4 then password <pw> and login
Assign management IP on a switch	interface vlan 1 then ip address <ip> <mask> and no shutdown
Add an interface description	interface <id> then description <text>
See all interface IPs and status	show ip interface brief
See port up/down and VLAN assignment	show interfaces status
See interface descriptions	show interfaces description
See running config	show running-config
See saved startup config	show startup-config
Save config	write memory
Reload a device	reload
