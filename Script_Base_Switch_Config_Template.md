enable
config t

! -- HOSTNAME --
hostname DS-07-SW1

! -- BANNER --
banner motd #Castle Rysen Ops: Authorized engineers only.#

! -- SECURITY AND PASSWORDS --
enable secret CrC0ffee!
service password-encryption

! -- CONSOLE LINE --
line console 0
 password VaultAccess
 login
exit

! -- VTY LINES --
line vty 0 4
 password ShelterAccess
 login
exit

! -- MANAGEMENT INTERFACE --
interface vlan 1
 ip address 192.168.10.11 255.255.255.0
 no shutdown
exit

! -- UPLINK INTERFACES --
interface range ethernet 0/0 - 1
 description ## Uplink to DS-07-SW2
exit

! -- SAVE CONFIGURATION --
end
write memory
