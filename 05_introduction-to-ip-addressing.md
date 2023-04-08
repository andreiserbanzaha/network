# Introduction to IP addressing

- IP addressing takes place in the *Network Layer*

## What is an IP address?

- is the address that is used on the network layer of the OSI model
- Network Layer needs to be able to move traffic from one device on the internet
    to some other device on the internet
- every single device that's connected to the internet MUST have a unique
    identifier at the Network Layer

- an **IP address**:
    - made out of 4 numbers (between 0 and 255) separated by dots
        - e.g. 203.0.113.10
    - this address is broken into components that help us identify where it is
        on the internet:
        - **Network Portion** -> **203.0.113**.10
        - **Host Portion** -> 203.0.113.**10**
    - it is a 32-bit address broken into 4 bytes(octets)

- how do we identify the Network and Host portions?
    - classful adressing (~1995 and prior)
    - classless addressing (~1995 to present)

## Classless addressing

- **Subnet Mark**
    - determines the network and host portions of the address
    - create a secondary address
        - network portion -> all binary 1s
        - host portion -> all binary 0s
        - **Subnet Mask + IP address** -> the **division line between the
            network and the host portion**
    - the Subnet Mask can be set almost anywhere within the 32 bits of the
        address (has to respect some rules)

- **example 1** -> first 24 bits -> Network Portion, last 8 bits -> Host
    - IP address:  203.0.113.10  -> 11001011.00000000.01110001.00001010
    - subnet mask: 255.255.255.0 -> 11111111.11111111.11111111.00000000

- **example 2** -> first 8 bits -> Network Portion, last 24 bits -> Host Portion
    - IP address:  10.0.0.10 -> 00001010.00000000.00000000.00001010
    - Subnet Mask: 255.0.0.0 -> 11111111.00000000.00000000.00000000

- **example 3** -> first 20 bits -> Network, last 12 bits-> Host
    - IP address:  10.0.0.10     -> 00001010.00000000.00000000.00001010
    - Subnet Mask: 255.255.240.0 -> 11111111.11111111.11110000.00000000
    - if subnet mask does not end on a byte, calculating networks and their
        respective addresses is a little more complex

## Classful Addressing

- how IP addressing was initially designed
- it was not designed to use a subnet mask

- **Unicast** addresses -> still the case today
    - class **A**: 0.0.0.0   -> 127.255.255.255
    - class **B**: 128.0.0.0 -> 191.255.255.255
    - class **C**: 192.0.0.0 -> 223.255.255.255
    - class **D**: 224.0.0.0 -> 239.255.255.255 -> only Network Portion
    - class **E**: 240.0.0.0 -> 255.255.255.255 -> experimental address range
        - not used at all

- the only usable public internet range is between *0.0.0.0 -> 223.255.255.255*
    - there are some exceptions that we cannot use on the public internet

## Address Types

- **Network Address**
    - identifier for a group of devices in a system
    - kind of like a zip code without the street address associated with it
        - zip code -> geographical area
        - network address -> range of IP addresses in an area
    - "Network prefix"

- **Broadcast Address**
    - identifier for all devices on a network
    - send a message to all the devices in a specific range of IP addresses
    - not used very much in layer 3

- **Host Address**
    - identifies a unique device on a network
    - used when communicating on an IP network

## Network Address

- **Network Address**
    - all binary **0**'s in the *Host* portion of the address

- **Broadcast Address**
    - all binary **1**'s in the *Host* portion of the address

- **Host Address**
    - everything in between all **0**'s and all **1**'s in the *Host* portion
        of the address

- example 1:
    - IP address:  203.0.113.55  -> 11001011.00000000.01110001.**00110111**
    - subnet mask: 255.255.255.0 -> 11111111.11111111.11111111.**00000000**
        - *host portion* are the last 8 bits
        - last 8 bits are not 00000000 or 11111111 -> it is a *host address*

- example 2:
    - IP address:  192.168.10.255 -> 11000000.10101000.00001010.**11111111**
    - subnet mask: 255.255.255.0  -> 11111111.11111111.11111111.**00000000**
        - *host portion* are the last 8 bits
        - last 8 bits are all 11111111 -> it is a *Broadcast address*


- example 3:
    - IP address:  10.10.0.0   -> 00001010.00001010.**00000000.00000000**
    - subnet mask: 255.255.0.0 -> 11111111.11111111.**00000000.00000000**
        - *host portion* are the last 16 bits
        - all 16 bits are 00000000 -> it is a *Network address*

- example 4:
    - IP address:  10.128.224.64   -> 00001010.10000000.11100000.010**00000**
    - subnet mask: 255.255.255.224 -> 11111111.11111111.11111111.111**00000**
        - *host portion* are the last 5 bits
        - all *host portion* bits are 0's -> it is a *Network Address*

- example 5:
    - IP address:  10.128.225.0  -> 00001010.10000000.1110000**1.00000000**
    - subnet mask: 255.255.254.0 -> 11111111.11111111.1111111**0.00000000**
        - *host portion* are the last 9 bits
        - not all bits are 0's or 1's -> it is a *Host Address*


## CIDR (Classless Inter-Domain Routing) notation

- used in order to make writing and saying subnet masks easier
- add to the IP address a slash and the number of bits with the value **1**
    from the subnet mask (the network portion)

- example:
    - IP address:  203.0.113.10  -> 11001011.00000000.01110001.00001010
    - subnet mask: 255.255.255.0 -> 11111111.11111111.11111111.00000000
    - using CIDR notation -> 203.0.113.10 **/ 24**

## Private IP Addresses

- private IP addresses range:
    - **10.0.0.0    -> 10.255.255.255**  (10.0.0.0/8)
    - **172.16.0.0  -> 172.31.255.255**  (172.16.0.0/12)
    - **192.168.0.0 -> 192.168.255.255** (192.168.0.0/16)

- these are **not routable** on the public internet
- these must be used in home networks, labs, enterprise networks etc.
- *network address translation* -> takes private address and temporarily
    converts it into a public address so you can communicate on the internet

- 169.254.0.0/16 -> APIPA
    - automatic private IP adressing
    - Microsoft Windows use this to try to help non-technical users
        automatically configure IP address on their network
    - don't really work -> should be avoided!

- there's no place like **127.0.0.1** (home) -> *The Loopback Address*
    - used to test to see if the IP or TCP/IP stack on the OS is working
        correctly
    - local address
    - used for testing on your local system

## Modify and test IP configuration

- use **ping** to test network connection

- in order for 2 devices to communicate with each other using IP addresses:
    - the 2 devices MUST be on the same IP network!
        - e.g.: **192.168.10**.10 and **192.168.10**.11 -> all good
        - e.g.: **192.168.11**.10 and **192.168.10**.11 -> not good, not on the
            same network!
    - if the devices are not on the same network -> add another device to
        facilitate the communication between those 2 networks -> **router**

- **Gateway** == **Router** !!!
