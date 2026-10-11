# Cisco Hardware
- Flash: where Cisco IOS image and other data live
- RAM: Boot copies flash to RAM, which is temp working memory where the IOS runs. where `running-config` is stored, which is volitile memory, which means if device looses power or reloaded without saving, it is lost. 
- ROM: Sotres the bootstrap
- ASICs: Application speciific integrated circuts
- Bootup: Flash is weakpoint, it has a lifespan. Restart can find that flash is bad. But bootup sequence is diagnostic if something fails.
- NVRAM:NonVolitileRAM Where the `startup-config` or saved config is stored, have to save things. 
- Erase `startup-config` from NVRAM: After erasing the startup-config, the running-config is still in RAM. Until you reload the device, the current configuration remains active. You can still save the running-config back to NVRAM with `copy running-config startup-config` before reloading to undo the erase.
