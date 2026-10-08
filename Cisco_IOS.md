# Cisco IOS CLI Modes

## User Mode `>`
- Press enter to get in to user mode 
- `?` ex `? ping` help manual

## Privileged Mode
- `enable` goes into `#` privileged mode
- `enable secret` to allow only authenticated staff, type `end` then `disable` to drop back to user EXEC, and `enable` to re-enter privileged EXEC and re-enter password


### Global Configure Mode
- `configure` to enter global configuration mode
- `hostname` to change name of switch
- `configure terminal` can edit module/port interface like speed

#### Interface 
- `interface fastEtherent`
- ports are module/port EX module 0 and interface 1 is 0/1
- `descrption` writes a note on the port. EX  `description "playground WAP"`
- `shutdown` turns off that module/port, `no shutdown` turns it back on

## Navigation from Global Configure mode
- `Exit` takes you back one level at a time
- `End` / `CTRL + Z`
- Arrows up arrows show command history
- Tab 

### Show
## Show Run
- `show run` shows all commands entered into the switch
- `show running config` shows hostname and interface descriptions

## `show IP interface brief` 
- `show run` 
- `show ip interface brief` shows all ports and if they are up or down
