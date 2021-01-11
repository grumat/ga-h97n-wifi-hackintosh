# USBMap.kext

This codeless kext injects the port map and power properties for the XHC on our H97N-WIFI.

```Info.plist``` will require edits and should have:
* no more than **15** ports in the ```ports``` dictionary
* a ```model``` that matches ```PlatformInfo```&#8594;```SystemProductName```  in the OC config.plist e.g. ```iMac14,2```
* a ```port-count``` that corresponds not to the total number of ports, but to the highest ```port``` address value present in in the ```ports``` dictionary e.g. ```0x15000000``` or ```FQAAAA==```

More Info: https://github.com/corpnewt/USBMap

## Port Physical Locations

### USB 2

| Port | Location                                        |
|:-----|:------------------------------------------------|
| HS01 | USB 3 Internal Header                           |
| HS02 | USB 3 Internal Header                           |
| HS03 | Rear Panel USB 3 Connector (near HDMI - below)  |
| HS04 | Rear Panel USB 3 Connector (near HDMI - over)   |
| HS05 | \*USB 2 Internal Header                         |
| HS06 | \*USB 2 Internal Header                         |
| HS07 | Rear Panel USB 2 Connector (at PS2 - over)      |
| HS08 | Rear Panel USB 2 Connector (at PS2 - below)     |
| HS09 | Rear Panel USB 3 Connector (near Audio - below) |
| HS10 | Rear Panel USB 3 Connector (near Audio - over)  |
| HS11 | Bluetooth slot (VID_8087&PID_07DC)              |
| HS12 | \*Unconnected                                   |
| HS13 | \*Unconnected                                   |
| HS14 | \*Unconnected                                   |

\* either 9 pin connector or mini PCIe, untested

### USB 3

| Port | Location                                        |
|:-----|:------------------------------------------------|
| SS01 | USB 3 Internal Header                           |
| SS02 | USB 3 Internal Header                           |
| SS03 | Rear Panel USB 3 Connector (near HDMI - below)  |
| SS04 | Rear Panel USB 3 Connector (near HDMI - over)   |
| SS05 | Rear Panel USB 3 Connector (near Audio - below) |
| SS06 | Rear Panel USB 3 Connector (near Audio - over)  |

### Back Panel USB Layout

```
 -------------------------------------------------------------------------
|  ------                                 __--__    __--__     ..     ..  |
| | HS07 |    .-.     .-.                | LAN2 |  | LAN1 |   (Or)   (LI) |
| |======|   (SMA)   (SMA)               | .... |  | .... |    ˜˜     ˜˜  |
| | HS08 |    ˜-˜     ˜-˜     ________    ======    ======     ..     ..  |
|  ------                     \=HDMI=/    ------    ------    (Bk)   (LO) |
|    --     ---------------     ˜˜˜˜     | SS04 |  | SS06 |    ˜˜     ˜˜  |
|  / PS \  | ######### ### |  ________   |======|  |======|  |˜˜˜˜|   ..  |
|  \ /2 /  | ######### ### |  \=HDMI=/   | SS03 |  | SS05 |  |TosL|  (Mi) |
|    --     \-------------/     ˜˜˜˜      ------    ------    ----    ˜˜  |
 -------------------------------------------------------------------------
```

# 15 Port Limit

Disable the ports you aren't using by removing them from USBPortInjector.kext/Contents/Info.plist

**Example:** If you are not using the internal 2.0 ports, then removing HS05, HS06, HS11, HS12, HS13, HS14 = 14 ports
