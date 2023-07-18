# TCP 3-Way Handshake

```
|--------------------------------------------------------|
|No. | Address | Packet  |  SEQ  |  ACK | Next SEQ | Len |
|--------------------------------------------------------|
|  0 | Client  | SYN     |     0 |      |        1 |  0  |
|--------------------------------------------------------|
|  1 | Server  | SYN ACK |     0 |    1 |        1 |  0  |
|--------------------------------------------------------|
|  2 | Client  | ACK     |     1 |    1 |        1 |  0  |
|--------------------------------------------------------|
```

## SYN
The first packet in the 3-way handshake is the client attempting to connect to the server. The client sends an initial SYN packet with a SEQ number of 0.

## SYN/ACK
The server responds to the SYN packet with a SYN/ACK, and starts it's own SEQ number at 0. The serveracknowledges receipt by sending back an ACK with the value of the server's SEQ + 1.

## ACK
The client receives the server's AYN/ACK and acknowledges receipt by sending back an ACK with the value of the server's SEQ + 1.

