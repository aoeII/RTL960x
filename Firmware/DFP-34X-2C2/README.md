# ODI DFP-34X-2C2
1. This for stick using Realtek `RTL9601D` SoC only!
2. If your stick using ZTE chipset, this firmware are not compatible!

# 4-port Emulation
| Firmware                         | Mode | 4-port Emulation |
|----------------------------------|------|------------------|
| `M114_sfp_ODI_210702.tar`        | IGD  | ❌ |
| `M114_sfp_ODI_220304.tar`        | SFU  | ✔️ |
| `M114_sfp_ODI_Vlan_220414.tar`   | SFU  | ✔️ |
| `M114_sfp_ODI_hybrid_220527.tar` | IGD  | ❌ |
| `M114_sfp_ODI_220817.tar`        | SFU  | ✔️ |

# `M114_sfp_ODI_220817.tar`
This firmware has custom fix and script, options are:

## Files
1. `fix_speed.sh` fix slow upload speed when using HiSGMII or 2500base-X
2. `fix_sw_ver.sh` allow custom software version when using `OMCI_OLT_MODE 3`
3. `fix_vlan_tag.sh` VLAN Tag Fix by @inyourgroove

## Activation
1. Enable `fix_speed.sh` execute `echo 1 > /etc/config/fix_speed` and `LAN_SDS_MODE` 4/5/6
2. Enable `fix_sw_ver.sh` require `OMCI_OLT_MODE 3` (custom software version)
3. Enable `fix_vlan_tag.sh` execute `echo 1 > /etc/config/fix_vlan`

> File `fix_sw_ver.sh` by @stich86 has upgraded, it will check `sw_custom_version0` & `sw_custom_version1` before apply, if empty, it will use `sw_version0` and `sw_version1` to prevent crash.

# SFU Mode
Switch Fabric Unit, ONU in Bridge Mode, Multiple VLAN, Internet provided by specific LAN Ports
![SFU](../../Docs/Images/xPON%20OMCI%20MIB%20SFU%20Mode.png)
If your ONU only in Bridge Mode, you need to use SFU firmware such as `M114_sfp_ODI_220304.tar`

# IGD Mode
Internet Gateway Device, ONU in Router Mode, ONU is Internet Gateway, having active DHCP, PPPoE Client, etc...
![IGD](../../Docs/Images/xPON%20OMCI%20MIB%20IGD%20Mode.png)
If your ONU has Wi-Fi, Internet, you need to use IGD firmware such as `M114_sfp_ODI_210702.tar`
