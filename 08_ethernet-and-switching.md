# Ethernet and switching

- located in the *Data Link Layer* (layer 2)
    - responsible for protocols that allow traffic to move inbetween devices
        that are locally connected together


## Ethernet

- incredibly prolific in data networking
- can be:
    - wireless
    - wired (ethernet switches)


## Carrier Sense Multiple Access with Collision Detection (CSMA/CD)

- creators of ethernet used to describe its operation
- collision domain -> a group of networked devices that will simultaneously
    detect a *voltage spike*(multiple devices sending data at the same time)


## Duplex and Speed

- the Duplex of a connection in Ethernet can be:
    - **half duplex** -> one device communicates at a time
        - just like a walkie-talkie -> only one person can speak at a time
    - **full duplex** -> two devices can communicate at the same time
        - just like a telephone
        - collisions are not possible

- modern collision domain -> half duplex connection between a PC and a switch
    - why do we have this: old device, old switch, experiment etc.
    - most modern networks are full duplex


## Ethernet II (2) frame

- Ethernet II -> protocol name
- this frame hasn't changed over time
- **frame**
    - mechanism that we use to move data across an ethernet network
    from one device to another
    - a chunk of data combined with data link layer header(e.g. ethernet header)
    - includes:
        - ethernet headers:
            - destination MAC address -> 48 bits (layer 2 address)
                - first 24 bits -> manufacturer ID
                - last 24 bits -> serial number
                - situated on the network interface card
            - source MAC address -> 48 bits (layer 2 address)
                - first 24 bits -> manufacturer ID
                - last 24 bits -> serial number
                - situated on the network interface card
            - type -> 16 bits
                - what type of data it's being transferred (layer-3 ? other?)
            - FCS -> 32 bits
                - cyclical redundancy check -> takes all the info in the frame,
                    runs an algorithm -> value -> put in the 32-bit field ->
                    when received by the other device -> same algorithm -> check
                    FCS to see if it's the same
        - data/payload (packet)
            - MTU -> Maximum Transmission Unit -> maximum 1500 bytes
            - layer-2 or layer-3 information

- **protocol Data Unit (PDU)** -> entire frame and the data transferred


## Network Topologies

- **Bus topology** -> single wire
    - tap into that single wire and run our devices off of that
    - very rare in modern networks

- **Ring topology** -> also deprecated

- **Star topology**
    - what modern Ethernet uses right now
    - initially used a Hub (multi-port repeater)
        - put a signal into it and all the other devices on that network hear it


### Layer-2 switch

- ethernet switches allow to prevent collision
- switches break up collision domains
- keep track of MAC addresses (table) -> read frame headers -> what source of
    MAC address is being received by a port -> use that to dispatch the messages
    for the Destination MAC address (assigned port) -> use a virtual circuit
- no other device hears that conversation


### Broadcast Messages

- very important in Ethernet
- Ethernet is considered to be a Broadcast network type
- all F's in the Destination MAC Address -> **Layer-2 Broadcast Address**
    - constantly used in the ethernet
- layer-3 broadcast addresses are very rarely used

- **Broadcast** -> when the destination MAC address of the frame is all F's, the
    frame is sent out to all active interfaces, except for the receiving one
- **Broadcast Domain** -> a group of networked devices which will receive a
    layer-2 broadcast message
