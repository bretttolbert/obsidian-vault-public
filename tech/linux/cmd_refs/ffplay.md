# ffplay

###### Play rtsps streams with ffplay

```bash
#!/bin/bash
CAM_URL_G4_BOTTOM_BACK_DECK=rtsps://192.168.0.196:7441/SGpBWR4rIFEdoiK2?enableSrtp
CAM_URL_G4_FRONT_PORCH=rtsps://192.168.0.196:7441/yPldDPLtkpX73yz8?enableSrtp
CAM_URL_G5_BASEMENT_BUNKER=rtsps://192.168.0.196:7441/DHKpHdqE5eZrr2Iy?enableSrtp
CAM_URL=$CAM_URL_G4_FRONT_PORCH
ffplay -fs -v warning -an -rtsp_transport tcp $CAM_URL
```

- `-fs` Play in full screen
- `tcp` Use TCP instead of UDP (default). TCP is required for Ubiquity UniFi cameras
