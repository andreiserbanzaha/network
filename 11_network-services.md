# Network Services

## Network Topologies

### Local Area Network (LAN)
- all the devices connected to the same network (on one side of the router)
    - e.g.: phones, PCs, switches
- may or may not include wireless

### Wireless Local Area Network (WLAN)
- all devices that are connected wireless to the same network

### Wide Area Network (WAN)
- connection between different buildings -> each with (possibly) multiple LANs
- 3rd party services required

- other WLANs:
    - Campus Area Network (CAN)
    - Metropolitan Area Network (MAN)

### Storage Area Network (SAN)
- giant system where layer-2 network technologies are used to connect large
    arrays of hard drives
- connect this storage area network up to all our servers (even in a virtualized
    server environment)
- allocate disk space for the servers right from the storage area network
- no need to have massive hard drives on each server in our data center

### Personal Area Network (PAN)
- connecting a small device to a computer (e.g. via Bluetooth)


## Network Address Translation

- critical to make the internet work
- private IP address ranges: 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16
    - build internal network using one of these address ranges or subnet of them
        - does not allow communication on the public internet -> must use a
            *public* IP address

- e.g. request to a public server (public IP address)
    - the server receives the request
    - source and destination IP addresses swap
    - destination IP is now *private* -> cannot be routed! -> thrown away

- solution -> **Network Address Translation (NAT)**
    - can be implemented both:
        - statically
        - dynamically -> **Port Address Translation**
            - uses a combination of both layer-3 and layer-4 addresses (IP
                address and port number) to keep track of unique conversations

    - example of *port address translation* (type of NAT -> dynamically)
        - message arrives to the router (which is configured to use *NAT*)
        - take away the private IP address, store it in a table temporarily
        - replace it with the public IP address of the external interface of the
            router (side that faces the internet)
        - message can then get to the destination and receive a response
        - replace router's IP with the one in the table
        - send message to the target device


## Port forwarding

- in order for a device out on the internet to be able to send a message
    directly to a device on the inside of your local network -> configure our
    router(connected to the internet) to say: "Hey, watch for traffic with these
    specific address properties. When a packet with these properties comes into
    the router, then do this special translation": **source socket** and
    **destination socket**
    - the router must be explicitly configured so that when it receives the
        message, it will change the public IP address with the IP of the device
        on that socket
        - requires manipulation of both the *packet header* at layer-3(IP
            address) and the *transport layer header* at layer-4(port number)

### Socket
- **an IP address + a transport layer port number**
- example:
    - source socket: 203.0.113.221:**59001** -> 10.0.0.10:59001
    - destination socket: 203.0.113.6:**9293** -> 10.0.0.20:9293


## Access Control Lists

- filter on specific IP addresses so that traffic cannot pass through or do some
    kind of manipulation on those messages


## Traffic Shaping

- based on *access control lists*
- *give/don't give* priority on the network to some traffic
- e.g. real-time conversations need to have priority

- methods of implementation:
    - **Quality of Service (QoS)**
        - Diffserv -> reprioritize traffic on each device
        - Class of Service
            - type of identifier for QoS


## Dynamic Host Configuration Protocol (DHCP)

- application layer protocol
- *allows automatic configuration of IP addresses on your network*
- typically there is a DHCP server build in and preconfigured with the Wireless
    router
- most networks have a DHCP server
- when manually configuring a DHCP server, we need to set up: an IP address, a
    subnet mask, a default Gateway and a DNS server
- a new device on the network:
    - discover message to the DHCP server
    - **DHCP offer**(ip, subnet mask, default gateway) from the DHCP server
    - **DHCP binding** -> record in a database of the MAC addresses of the
        devices on that network and their configuration so that it wont give
        the same IP address to the next devices connected
    - **DHCP lease** -> typically 7 days for DHCP servers

- e.g. printers have a manually (statically) configured address -> all the
    devices in that area can be configured to use the same printer at that
    specific IP address


## Domain Name Service (DNS) Hierarchy

### Uniform Resource Locator (URL)
- used to create a hierarchy in the domain name system
- **Top Level Domain (TLD)** (e.g.: ".com", ".net", ".org" etc.)
    - general category of the type of site this is
- **Second Level Domain**
    - domain name (e.g. "google", "pluralsight", "facebook" etc.)
- **Third Level Domain**
    - can be one of 2 things:
        - *hostname* of a specific device (e.g. "www" -> World Wide Web server)
        - *subdomain* (e.g. "www.**engineering**.university.edu") -> 4'th level
            domain is now the *host*

- the idea behind URL is to give DNS a hierarchy -> find an IP address for a
    specific URL

### Forward DNS Lookup
- cannot use the site name in the Destination IP
- use DNS protocol to lookup the IP address of the desired server
- DNS server will respond with the IP of the desired server

- there is a whole hierarchy of servers
- top-level domain servers -> holds all entries for all top-level domain names
    (.com, .net, .org, etc)
- if our default DNS server (e.g. google) doesn't know the web server we are
    trying to get to, it will ask the higher level DNS servers the IP address of
    that web server, return it to our device, and store it in its database
    temporarily -> next requests of the IP address of that web server -> it will
    have it locally


## Reverse DNS Lookup

- what is the domain for an IP address
- must be explicitly configured

- *DNS Record Types* -> keep track of a URL-to-IP address mapping(not everything
    is mapped to an IP address)
    - **A - IPv4 Record**
        - translates URL into IPv4 address
    - **AAAA - IPv6 Record**
        - translation from URL to IPv6 address
    - **CNAME - Canonical Name Record**
        - change request to be another domain name, do a lookup, and then return
            that IP address to that client (web servers are configured
            differently and they don't want you to go to "www.". Maybe they want
            you to go to "web.")
    - **MX - Mail Exchange Record**
        - used by mail servers in order to figure out how to route email around
            the internet
    - **NS - Identifies Authoritative Name Server**
        - ???
    - **PTR - Pointer Record**
        - similar to CNAME
        - doesn't automatically do the lookup for the client -> replies to the
            client that he has to go to this other URL
    - **SRV - Service Record**
        - point to a specific layer-4 or layer-7 service in DNS
    - **TXT - Text Record for miscellaneous use**
        - authentication utilities
        - encryption utilities(SPF, DKIM)

- external DNS:
    - e.g. google's DNS -> URL to Public IP address lookups
- internal DNS:
    - access internal, privately IP's devices
    - if internal DNS server doesn't know how to obtain the IP address for a
        specific web server -> request to external DNS to resolve
