# Introduction to IPv6

## Address sizes

- **Bit**: 1 or 0

- **Nibble** -> 4 bits (half a byte)
    - e.g. 1010 -> 0xA (hex)

- **Byte** -> 8 bits
    - e.g. 11001001 -> 0xC9 (hex)

- **Hextet** -> 16 bits
    - e.g. 10101010 01000110 -> 0xAA46 (hex)

- **IPv6 addresses are written in hexadecimal in sets of 4**

- IPv4 -> 32 bits long -> 4 octets
    - e.g. 192.168.10.10 (11000000.10101000.00001010.00001010)

- **IPv6 -> 128 bits long = 32 nibbles = 32 hexadecimal values = 8 hextets**
    - 4 times longer than IPv4
    - e.g. 2001:0DB8:0002:008D:0000:0000:00A5:52F5

- avoid binary when working with IPv6 whenever possible
    - designed this way

- 2 portions -> **Network** and **Interface Identifier**
    - typically divided at 64 bits -> **/64** mask on the network
        - not recommended to stray from this

- shorter version:
    - eliminate leading 0's
    - take successive hextets of 0's -> replace with **::** (double colon)
        - only use one double colon in an address
        - typically between the network portion and the host portion
            - easier to understand and set up

- e.g.
    - 2001:0DB8:0002:008D:0000:0000:00A5:52F5
    - 2001:DB8:2:8D:0:0:A5:52F5
    - 2001:DB8:2:8D::A5:52F5

## How many IPv6 addresses?

- host portion -> 2^64 ~ 18.000.000.000.000.000.000 addresses
- same for network portion

- there are 2 IPv6 addresses:
    - 1. **Unicast Address** -> global unicast address
        - allows communication onto the internet using IPv6
    - 2. **Link Local Address** -> only exists within the layer 2 network and
        never leaves it
        - kind of like a MAC address used at the Network Layer
        - unique identifier
        - never leave the Local Internet Network(just like MAC addresses - never
            routed off that network)
        - automatically configured

    - every single interface in IPv6, if it's going to talk on a routed network,
        will require at least 2 IPv6 addresses -> unique to IPv6

## IPv6 Address Acquisition

- **SLAAC** -> Stateless Address Auto Configuration

- e.g. PC connected to a Router (a Layer 3 device)
    - if the Router has an IPv6 address configured -> it's going to send this
        advertisement saying "Hey, I'm a router and I'm on this network:
        2001:DB8:4:A::1/64"
    - the PC will get that advertisement -> "Oh, I'm on network
        2001:DB8:4:A::/64"
        - *Windows*: the PC can then pick its own IP address
            - going to use: *Random 64 bit Interface Identifier*
                - e.g.: 2001:DB8:4:A:6784:5FC1:7B4C:A52A/64
        - *Unix/Linux/Mac* (standard version of unix code)
            - they are going to use: *Modified EUI-64* format for the address
                - 1. take the MAC address (48 bits long) -> modify to make it 64
                    bits long -> break in half and put in the middle: *FF:FE*
                - 2. take the first 8 bits -> convert to binary -> flip the 7'th
                    value (e.g. if it's 0 -> 1, if it's 1 -> 0) -> reconvert to
                    hexadecimal (e.g. 00 -> 02)
            - e.g.:
                - MAC address 000C:29FC:70A5 -> 000C:29FF:FEFC:70A5
                    -> 020C:29FF:FEFC:70A5 (host portion)
                - result address: 2001:DB8:4:A:**020C:29FF:FEFC:70A5**/64
            - send message back to the router -> "Hey, I'm a neighbor now,
                here's my address" -> router records the address in a table ->
                know which IPv6 address at layer 3 is associated with MAC
                address at layer 2


## IPv6 DHCP

- acquire IPv6 address -> use a DHCP server
- e.g.
    - PC connects to network -> "Hey, I'm new, I need IPv6 address"
    - the DHCP server will return an address

### Tunneling IPv6

- connect from IPv4 internet to IPv6 internet through **tunneling**

- tunnel from the IPv4 internet to the IPv6 internet -> allow access to it
    - take IPv6 packets and put them into IPv4 packets -> send across internet
    - when it arrives to the IPv6 internet -> unpack the IPv4 packet and take
        out the IPv6 packet

- Hurricane Electric ?
