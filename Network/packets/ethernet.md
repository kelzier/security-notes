# Ethernet frame

```
|----------------------------------------------------------------|
| Dest Mac | Source Mac | Ether type | Data            | FCS     |
|----------------------------------------------------------------|
| 6 bytes  | 6 bytes    | 2 bytes    | 46 - 1500 bytes | 4 bytes |
|----------------------------------------------------------------|
|                            1518 bytes                          |
|----------------------------------------------------------------|
```

## Data frame (IPv4)
```
|-------------------------------------|
| IP       | TCP Options | Payload    |
|-------------------------------------|
| 20 bytes | 20 bytes    | 1460 bytes |
|-------------------------------------|
|                MTU                  |
|-------------------------------------|
|                        |   MSS      |
|-------------------------------------|
|               1500 bytes            |
|-------------------------------------|
```

## Data frame (IPv6)
```
|-------------------------------------|
| IP       | TCP Options | Payload    |
|-------------------------------------|
| 40 bytes | 20 bytes    | 1440 bytes |
|-------------------------------------|
|                MTU                  |
|-------------------------------------|
|                        |   MSS      |
|-------------------------------------|
|               1500 bytes            |
|-------------------------------------|
```


## IPv4 Header (20 bytes)
```
|-------------------------------------------------------------------------------------|
|                                         Bits                                        |
|-------------------------------------------------------------------------------------|
|0       4|        8|        12|        16|        20|        24|        28|        31|
|-------------------------------------------------------------------------------------|
| Version |   IHL   |   Type of Service   |             Total length                  |
|-------------------------------------------------------------------------------------|
|           Identification                | Flags   |     Fragment offset             |
|-------------------------------------------------------------------------------------|
|  Time to live     |     Protocol        |       Header checksum                     |
|-------------------------------------------------------------------------------------|
|                                   Source address                                    |
|-------------------------------------------------------------------------------------|
|                                 Destination address                                 |
|-------------------------------------------------------------------------------------|
```

|            |          |
|------------|----------|
|**version**:| A 4-bit field describing the IP type used in the packet.| 
|**IHL**:| Internet Header length, a 4 bit field describing the length of the header. |
|**TOS**:| Type of Service, an 8 bit field  describing the type of service for the packet (i.e reliability, precedence, throughput, and delay).|
|**Total length**:| A 16-bit field that indicates the total size of the packet, with a maximum size of 65535 |
|**Identification**:| A 16-bit field that describes the identification number of a packet. If the data is fragmented, each piece will share the same value. |
|**Flags**:| A 3-bit field that enables fragmentation. The first bit is always 0, the second bit is set when data is fragmented, the third bit indicates there are more fragmented packets to follow.|
|**Fragment offset**:| A 13-bit field that determines to which part of the original packet this fragment belongs.|
|**Time to live**:| An 8-bit field that indicates the amount of time or the number of hops a packet can have before it is discarded.|
|**Protocol**:| An 8-bit field that specifies the upper layer protocol.|
|**Header checksum**:| A 16-bit field that calculates the checksum at every router hop. It is used to validate the header.|
|**Source address**:| A 32-bit field for the source IP address. |
|**Destination address**:| A 32-bit field for the destination IP address.|


## IPv4 Header (40 bytes)
```
|-------------------------------------------------------------------------------------|
|                                         Bits                                        |
|-------------------------------------------------------------------------------------|
|0       4|        8|        12|        16|        20|        24|        28|        31|
|-------------------------------------------------------------------------------------|
| Version |   Traffic class    |                      Flow label                      |
|-------------------------------------------------------------------------------------|
|                Payload length           |      Next header    |     Hop limit       |
|-------------------------------------------------------------------------------------|
|                                   Source address                                    |
|                                                                                     |
|-------------------------------------------------------------------------------------|
|                                 Destination address                                 |
|                                                                                     |
|-------------------------------------------------------------------------------------|
```

|            |          |
|------------|----------|
|**version**:| A 4-bit field describing the IP type used in the packet.| 
|**Traffic Class**:| An 8-bit field similar to the ToS field in the IPv4 header. The first 6-bits represent the service required for this packet, and the last 2-bits are used for Explicit Congestion Notification.|
|**Flow label**:| A 20-bit field used to label packets belonging to the same sequence to ensure packets are delivered in the correct order. |
|**Payload length**:| A 16-bit field that indicates the total size of the packet, with a maximum size of 65535 |
|**Next header**:| An 8-bit field that indicates the type of the first extension header |
|**Hop limit**:| This is the same as the TTL field in the IPv4 header. It indicates the number of hops a packet can take before being discarded.|
|**Source address**:| A 128-bit IP address of the source device.|
|**Destination address**:| 128-bit IP address of the destination device. |