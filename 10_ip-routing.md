# IP routing


## OSI Model - Network Layer

- *Data link layer* is responsible for moving traffic in little network segments
    in the local area networks
    - switches keep a MAC addresses to know where to forward frames

- **Network layer** is responsible for getting traffic across the network, from
    one LAN to another LAN (from one Ethernet segment to another) or from one
    VLAN to another VLAN -> **IP Routing**
    - responsible for end to end communication -> from our workstation to the
        server that we're communicating with

- **Routers**
    - wireless routers -> provide wireless signal
    - functioning as a multi-purpose device
    - always uses a circle with 4 arrows inside (pointing in opposite direction)
        as a icon
    - layer-3 device
    - internet is full of routers


## Basic Network

### Routers
- they have at least 2 interfaces on them -> at least 2 ports where we can
    plug in a cable of some kind, in order to build a *data link layer*
    connection into the router
    - just like a PC with at least 2 network interface cards
    - the interfaces are going to point to:
        - internal devices
        - the internet
    - each interface is going to be on a unique IP network:
        - one is going to be on a unique subnet that has all 0's in the *host
            portion* -> individually assign IP addresses directly to each *host*
            in our system (e.g. internal IP: 10.0.0.0/24)
        - one is going to be outside of the network (e.g. 203.0.113.4/30)
    - configuring it like this -> internal devices can communicate with each
        other and out to the internet and back again

### The IP Packet
- the internet protocol is specifying:
    - how the IP addressing works
    - how to construct a header to put on the data that we're trying to transfer
        from one device to another

- **ICMP Protocol** -> Internet Control Message Protocol
    - used by *ping* in order to send messages
    - contains:
        - *source IP address*
        - *destination IP address*
        - *TTL* -> time to live value
            - how many routers the packet has traversed in order to reach
                its destination
            - if the TTL value hits 0, it will be thrown away -> prevent
                loops at layer-3
        - other

- **packet** -> word used specifically at the *Network Layer*
    - a header + some data that we're carrying at the network layer
    - this packet is put inside a *frame* at layer-2 that contains:
        - *Destination MAC address* -> obtained through ARP
        - *Source MAC address* -> added when it's sent
        - *Layer-3 protocol* -> e.g. IPv4
        - *FCS* - frame check sequence

### Address Resolution Protocol (ARP)
- help retrieve a layer-2 MAC address using a layer-3 address
    - keeps an ARP Table (Cache) - for about 90 seconds -> age out
    - the *ARP Table* **is NOT** the *MAC Address Table*
    - the *ARP TAble* exists on devices that have both a Layer-2 and a Layer-3
        address ????
    - *MAC address table** -> purely a Layer-2 table that maps a MAC address
        that's connected to a specific switch port on a Layer-2 switch
    - *ARP Table* -> bridge between Layer-2 and Layer-3
- it's purely a layer-2 protocol
- how ARP requests work:
    - builds a frame that contains:
        - *destination MAC address* -> all F's -> broadcast message
        - *source MAC address* -> of the device from which is being sent
        - *ARP* -> specify protocol type
        - *data* -> "Who has the MAC address for IP: 10.0.0.20" ?
    - message goes to all the devices on *our* network except to the device that
        sent the request
    - when the device with that IP receives the message, it will create a new
        frame containing:
        - *destination MAC address* -> the one received in the request
        - *source MAC address* -> of the device
        - *ARP* -> specify protocol type
        - *data* -> the MAC address of the device (same as source)
    - the initial computer will receive the response and can then set the
        *destination MAC address* in the frame, and then send the *ping* message
    - the switch will then dispatch the message to the destination device
    - then the other computer does the same process in reverse (the ARP) to
        respond to the *ping* message

- the only devices that are going to respond to an ARP request, are going to be
    the devices that are on that same network !!!


## Demo: ARP Table

- e.g. on the *192.168.10.0* network
    - broadcast network IP: *192.168.10.255/24*
    - Layer-2 broadcast address -> physical/MAC address -> *ff-ff-ff-ff-ff-ff*


## The Default Gateway

- there are 3 pieces of information that are configures on our workstation:
    - IP address
    - subnet mask
    - default gateway/router

- is the exact same thing with the *router*
- it's the place where our device sends traffic to when it does not know how to
    reach the destination network
    - the IP address that we're trying to reach is on a different subnet than
        the one that our device is on
- routers explicitly throw away broadcast messages at layer-2 (if the
    destination MAC address is filled with F's)
    - they will receive and process the broadcast message, but they will NOT
        forward the message on
- in order to get the message on another network -> ARP our default gateway
    - send a ARP request to find the router MAC address
    - create the frame with the destination MAC address of the router
    - when the message arrives to the router
        - router checks its routing table in order to see if it knows how to
            reach its destination
        - if it finds the IP network, it will check at which port is that IP
            configured and connected (e.g. F0/1 interface)
        - rebuild the *frame*
            - add source destination of the Fast Ethernet's MAC address (the
                port one where the IP is configured)
            - change TTL value from 128 to 127
            - ARP request to the other network
            - the device will respond with its MAC address
            - add the destination MAC address to the frame
            - send message to destination device

- the purpose here is to get the message onto other networks


## IP Routing

- packet header is used to identify the beginning and ending devices that are
    both sending and receiving the packet

- *layer-2 frame*  -> **short haul**(internal movement of that message)
- *layer-3 packet* -> **long haul**(source address to destination address)

- add routes to each router on the internet so that it knows how to reach all
    the networks in the system

- if there is no route in the routing table to the IP address the message is
    destined to, the packet will be thrown away

### Routing types

- configure routes -> how to propagate traffic to the next device

- **Static routing** -> manually
    - on each router to determine the next hop

- **Dynamic routing** -> automatically -> using a routing protocol
    - if there's a failure of a redundant link -> recalculate best path
    - dynamic routing protocols:
        - **RIP**(routing information protocol)
            - distance vector category
        - **EIGRP**(Enhanced Interior Gateway Routing Protocol)
            - distance vector category
        - **OSPF**(Open Shortest Path First)
            - link state category
        - **BGP**(Border Gateway Protocol)
            - primary routing protocol used on the internet
            - exterior routing protocol / exterior gateway routing protocol
            - allows internet service providers to create business contracts
                with each other -> routing plan based on the business contract
            - hybrid category


## Trace route (TRACERT)

- list of the routers the message went through until it reached its destination
