# Cisco IOS CLI Modes

## User Mode `>`
- Press enter to get in to user mode 
- `?` ex `? ping` help manual

## Privileged Mode `enable`
- `enable` goes into `#` privileged mode
- `enable secret` to allow only authenticated staff, type `end` then `disable` to drop back to user EXEC, and `enable` to re-enter privileged EXEC and re-enter password

### Global Configure Mode `configure` 
- `configure` to enter global configuration mode
- `hostname` to change name of switch
- `configure terminal` can edit module/port interface like speed
- `banner motd` message of the day, like don't log in please.
- `password` don't use, in plain text
- `secret` use, is hash, example `secret PASSWORD`
- `no` removes a configuration
- `end` or ctl `z` gets out of Global Config mode and back to Privileged Mode
- `line vty` virtual terminal, remote into switch.
- `copy running-config startup-config`


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

#### `show IP interface brief` 
- `show run` gives verbose info for all ports 
- `show ip interface brief` shows all ports and if they are up or down

## Example Switch/Router Base Config
- `hostname`
- `banner motd ?` 
- `enable password` 
- `line console` blocks user mode, on the console port/line, then set a `password` 
- `line vty` virtual terminal, remote into switch. Example `line vty 0 4` is for ports 1 though 5
- IP address via `interface vlan 1`
- `descriptions` write comment/description/note for a port via example `int fa0/1` and then `descrition` 
- `copy running-config startup-config` saves changes to base config or just write `wr`


