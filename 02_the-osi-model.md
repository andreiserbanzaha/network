# The OSI model (Open Systems Interconnections model)

- [1] Application Layer
- [2] Presentation Layer - not really needed anymore
- [3] Session Layer - not really needed anymore
- [4] Transport Layer
- [5] Network Layer
- [6] Data Link Layer
- [7] Physical Layer



## Physical Layer

- transmits **raw bits**
- convert binary sequences into signals
    - electric signal (copper cable)
    - light signal (fiber cable)
    - radio signal (air)
- transmit them over local medium
- used to connect all the devices together
- example:
    - workstation (laptop / pc)
    - router (wireless / cable)
    - cable modem (from ISP)
    - internet
    - server (e.g. https://www.pluralsight.com)

- from the workstation -> request for the pluralsight web page to the server
- the server pulls up the web page requested -> transfers to the workstation
- not all cables used in networking are identical
    - **twisted pair** cables
        - the ones used home or at the office (most likely)
        - fiber optic or proprietary copper cables
    - **CoAx** cable
        - modem to ISP (most likely)
- convert binary sequences into signals
    - electric signal (copper cable)
    - light signal (fiber cable)
    - radio signal (air)
- transmit them over local media

- Segments (data) -> Transportation Layer
- Packets (data, source IP, destination IP) -> Network Layer
- Frame (source MAC, destination MAC, Packets, FCS) -> Data Link Layer



## Data Link Layer

- protocols to move traffic from one end of the cable to the other end
    - move in short hops -> network segments

- **network segments** -> a collection of network devices that all operate in
    the same space with the same protocol
    - e.g. workstation -> router -> modem -> internet(many segments) -> server
    - each network segment use a specific network protocol to manage and
        transfer the data (most of them are Ethernet(either wired or wireless))
    - modem -> ISP: DOCSIS-3 (Data over cable service interface specification)

- **DOCSIS-3**
    - used by cable ISP's to connect to the internet

- **Ethernet**
    - permits extremely high speed communication
    - most of the internet uses Ethernet protocols
    - connect one ISP to another ISP

- **physical addressing**
    - data packet + MAC addresses of sender and receiver -> **frame**

- MAC address -> 12 digit alfa-numeric number
    - embedded in the network interface card in your computer by the computer
        manufacturer

- 2 basic functions:
    - access the media (for higher layers of the OSI model)
        - framing
    - controls how data is placed and received from the media
        - media access control -> Carrier-sense multiple access(CSMA)
        - error detection

- **Media/Medium Access Control (MAC)**
- **Logical Link Control (LLC)**



## Network Layer

- communicate from the workstation to a server (long distance)

- **IP addressing**
    - allow to send messages across longer distances on the network (end-to-end
        communication)
    - provides an **unique address** to all the devices on the internet!
    - kind of like a home address (country, state, city, zip code, str, nr)

- **IP routing**
    - allow to send messages from one unique address on the internet to any
        other unique address on the internet

- data units (segments) are called **packets** in the network Layer
- the function of network layer:
    - **logical addressing** (IPv4, IPv6)
        - assigns IP addresses to each segment to form an IP packet so that each
            segment can reach the correct destination
    - **routing**
        - moving data packet from source to destination
        - based on logical addressing of IPv4 / IPv6 + Mask(255.255.255.0)
            - 255 -> represents the network
            - 0 -> represents host or receiving computer
    - **path determination**
        - protocols: OSPF, BGP, IS-IS
        - finds best possible path for data delivery

- mapping between physical addresses and logical addresses
- **Address Resolution Protocol (ARP)**



## Transport Layer

- session between client and server

- controls the reliability of the communication through:
    - **segmentation**
        - data received from the session layer is divided into small data units
            called **segments**(source, destination, port nr, sequence nr)
            - port number -> helps to direct each segment to the correct app
            - sequence number -> helps to reassemble segments into the correct
                order (to form the correct message to the receiver)
    - **flow control**
        - the amount of data being transmitted
        - e.g. transmission protocol tells server to limit the transfer speed to
            the maximum the receiver can handle (so that no data gets lost), or
            increase speed if server sends with lower speed
    - **error control**
        - if missing data -> **Automatic Repeat Request** -> retransmit the lost
            or corrupted data
        - **checksum** - added to each segment to find out the received
            corrupted segment

- **Transmission Control Protocol (TCP)**
    - allows to build session between client and server -> then ask for data
    - connection-oriented transmission
    - has feedback -> lost data can be retransmitted

- **User Datagram Protocol (UDP)**
    - connectionless transmission
    - no feedback
    - is used where it does not matter whether it has received all data
        - e.g. streaming, videogames, movies, TFTP, DNS



## Session Layer

- Citrix ICA protocol
- firewall, troubleshooting etc.
- also operating at the **Application Layer**

- setting up and managing connections (sending / receiving data)
- termination of connections / sessions

- helpers: APIs (Application Programming interfaces)
    - e.g. NETBIOS (API -> enables for computers to communicate with each other)

- **authentication** -> before the sessions starts -> server performs
    authentication to check who you are (username and password)
- **authorization** -> determines if you have permission to access a file or not

- **session management** -> keeps track of the files that are being downloaded

- web browser uses:
    - Application Layer
    - Presentation Layer
    - Seesion Layer

- construction, direction and conclusion of connection between devices occur
- authentication and re-connection if a network interruption occurs



## Presentation Layer

- not that important with modern networking
- convert IBM's EBCDIC(ASCII equivalent) to ASCII
    - nowadays these are done in the application layer (if needed)

- translation -> e.g. IBM's EBCDIC(ASCII equivalent) to ASCII
- data compression -> can be lossy or lossless
- encryption/decryption -> **Secure Sockets Layer (SSL)**

- syntax processing (convert data from one format to another)
    - application format -> network format and vice-versa
    - converting / encryption



## Application Layer

- getting the website from the server to the client

- **Hypertext Transfer Protocol (http)**
    - protocol that allows to transfer the website located on the server to the
        web browser located on the client
    - web pages are written in a protocol called Hypertext (file)
        - basic formatting of a text document to indicate instructions on how to
            present information in the web browser

- **https** - encrypted version

- responsible for moving the desired application from the server to the client

- it is used by network applications (computer applications that use internet)

- protocols: HTTP, HTTPs, FTP, FMTP, NFS, DHCP, Telnet, SNMP, POP3, IRC, NNTP

- these protocols form the basis for various network services:
    - file transfer -> FTP protocol
    - web surfing -> HTTP/HTTPs protocols
    - emails -> SMTP protocols
    - virtual terminals -> Telnet