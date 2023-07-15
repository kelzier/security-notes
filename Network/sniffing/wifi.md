# WiFi

## Monitor mode
Either:   
```
airmon-ng start wlan0
```

Or:  
```
ifconfig wlan0 down
iwconf wlan0 mode monitor
ifconfig wlan0 up
```


## Capture frames
`airodump-ng wlan0mon`

## Capture MAC addresses
To capture the MAC address of clients who have authenticated to the AP:  

`airodump-ng -c <channel> -a -bssid <bssid>`

Where:   
`<channel>` - The Channel that the AP is broadcasting on   
`<bssid>`   - The BSSID of the AP

## Spoof MAC address
Once a MAC address has been determined, the local MAC can be changed. First you need to take down the local adapter:

`ifconfig wlan0 down`

Then you can use `macchanger` to change the MAC address to match the one you captured:

`macchanger -m <mac> wlan0`

Finally, bring the interface back up:

`ifconfig wlan0 up`

