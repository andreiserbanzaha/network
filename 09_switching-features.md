# Switching features


## Connecting switches

- connect multiple switches (layer-2 switch) -> increase the size of the
    broadcast domain (layer-2 broadcast)
    - other switches that are connected are also going to receive the broadcast
        message which will be forwarded to the devices connected to THAT switch

- broadcast messages:
    - get sent to all the interfaces that are active
    - get propagated out all active switchports

- if 2 switches are connected with 2 cables:
    - one switch will send a broadcast message
    - the other switch will receive 2 messages (since 2 ports are connected)
    - the switch receiving the 2 messages *will forward the messages back to
        the switch that has sent the broadcast messages* -> broadcast messages
        get stuck in between the 2 switches -> infinite loop -> in time it will
        crash the network -> *broadcast storm*

- **Broadcast storm** -> too much traffic between switches
    - solution: Radia Perlman's **Spanning Tree Protocol (STP)**
        - figures out which ports are redundant -> shut one of them down -> only
            use one connection in between the switches
        - only on higher end switches


## Intro to VLANs

- each broadcast domain represents one single layer-3 network

- **LAN** -> local area network
    - group of devices connected together with an ethernet switch

- **VLAN** -> virtual LAN
    - support more than one broadcast domain
    - each of the switchport from a VLAN switch has a number assigned to it
        - configure each switch port to be assigned to a specific VLAN
        - isolate traffic within the network

- **Trunk Link** -> link designed to connect switches that are using VLAN
    together
    - *tagged/untagged ports/links*
        - tagged(trunk) on the VLAN configured ports
        - untagged(access) on the other ports (where PC connects to switch etc.)

- e.g. multiple switches connected together with multiple VLANs
    - switches are connected through a **Trunk Link**
    - messages that travel between switches through a Trunk Link
        - added additional information to the *frame header* -> the **VLAN tag**
        - removed when it arrives at the end of the Trunk link -> switch can
            dispatch the message to the devices that are configured on that VLAN


## Switch Port Mirroring

- utility that we can use to collect traffic for analysis when experiencing some
    kind of problem on the network
- monitor traffic to see that it's legitimate
    - connect an intrusion detection device to a mirrored port -> analyze
        traffic -> run through algorithms to check if it's legitimate

- e.g. Wireshark


## Power over Ethernet (PoE)

- deliver power through the Ethernet cable
- protocols: **802.3af** and **802.3at**
