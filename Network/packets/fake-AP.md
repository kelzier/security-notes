# mdk 

Either:
    airmon-ng start wlan2
Or:
    ifconfig wlan2 down
    iwconf wlan2 mode monitor
    ifconfig wlan2 up


mdk4 <interface> b -c <channel> -f <file>
mdk4 wlan2 b -c 11 -f fake-net


