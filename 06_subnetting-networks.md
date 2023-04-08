# Subnetting networks

- **subnetting** -> breaking large network into smaller networks

## Components of an IP network and Subnetting basics

- **Network IP Address**
    - all binary 0's in the *Host portion*

- **Broadcast IP Address**
    - all binary 1's in the *Host portion*

- **Host IP Address**
    - everything that is not a Broadcast or a Network Address

### Subnetting basics

- every area within an organization will get its own unique IP network

- 10.0.0.0/8 -> private IP address range (since it ends with 0)
    - Network address:   00001010.00000000.00000000.00000000
    - Broadcast address: 00001010.11111111.11111111.11111111
    - subnet mask:       11111111.00000000.00000000.00000000

    - very massive potential for host addresses (~16 million) -> too much
        - range: 10.0.0.0 -> 10.255.255.255

    - if we take *10.0.10.0* (host address) -> last 8 bits are all 0's
        - move the subnet mask to /24 -> a new network address -> 10.0.10.0/24
            - network address:   00001010.00000000.00001010.00000000
            - broadcast address: 00001010.00000000.00001010.11111111
            - new range: 10.0.10.0 -> 10.0.10.255
            - much more manageable subnet to assign to a group of devices

- **variable length subnet masking (VLSM)**
