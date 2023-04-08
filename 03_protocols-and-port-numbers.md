# Protocols and port numbers

- application layer protocols:
    - data transfer protocols
    - authentication protocols
    - network service protocols
    - network management protocols
    - audio/visual protocols

## Transferring data: HTTP or HTTPs

- http / https -> hypertext transfer protocol (secure)
    - secure -> all data is encrypted (from client to server)

- almost all application layer protocols use the model of having a client and a
    server

- transferring a file in the format of hypertext(formatting a file in a way
    that's readable by a web browser)

- web browsers (clients): Chrome, Firefox, Safari etc

- web servers: Apache, nginx -> server side software for websites
    - host websites on the internet

- web servers and web browsers work together to transfer these hypertext
    documents in order to get the website from the server to the client

- every single layer 7 (application) protocol has a layer 4 component -> **port
    number** -> uniquely identifies the layer 7 protocol being used at layer 4
    - use these port numbers to easily identify traffic at level 4 so that
        computing systems can understand how to interpret the traffic and what
        layer 7 protocol to send the messages to
        - **http** -> port number **80** (transport layer protocol)
        - **https** -> port number **443** (transport layer protocol)

## File transfer protocols: FTP, sFTP, TFTP

- transfer files from a *client to server* or *from server to client*

- **FTP** / **sFTP** - (secure) file transfer protocol
    - are used to transfer files from one device to another
        - there is client and server software designed to do this
    - require username and password
    - sFTP -> encrypt the traffic

    - FTP -> port numbers **20** and **21**
        - one is used for authentication
        - one is used for transferring information

    - sFTP - port number **22** (also the port for **SSH** - secure shell)
        - take FTP protocol and put it inside an SSH session (encrypt traffic)

- **TFTP** - trivial file transfer protocol
    - meant for sending tiny files between 2 devices
    - have simple setups to transfer files quickly without having worry about
        authentication or having issues with firewalls causing traffic to be
        knocked down
    - does not require username or password
    - port number **69**

- *filezilla* -> FTP client (application) -> connect to an FTP server
    - e.g. "ftp://10.128.50.116" -> server address

- **SMB** - server message block
    - port number **445**
    - shared/common files within a network (e.g. within an enterprise)
        - mount a drive locally (e.g. "\\serverName\share") -> map the "share"
            folder to the workstation -> access to the shared files

## Email: POP3, IMAP, SMTP

- **POP3** - post office protocol
    - port numbers: **110** for unencrypted and **995** for encrypted
- **IMAP** - internet message access protocol
    - port numbers: **143** for unencrypted and **993** for encrypted
- **SMTP** - simple mail transfer protocol
    - port numbers: **25** for unencrypted and **465** for encrypted

- POP3 and IMAP -> used by a client to retrieve mail from a server
- SMTP -> send an email to an SMTP server -> forward the email to destination

## Authentication (LDAP, LDAPs) and Network Services (DHCP)

- **LDAP/LDAPs** -> Lightweight Directory Access Protocol (secure)
    - port numbers:
        - LDAP -> **389**
        - LDAPs -> **636**

- authenticate to the network, bring all mapped network drives and settings

- **DHCP** -> Dynamic Host Configuration Protocol
    - transferring data -> little bits of information that allow the network to
        work properly
    - automatically hands out IP addresses to any device that's connected

    - how this works:
        - workstation (laptop, mobile phone etc.) sends a message to the DHCP
            server to request an IP address
        - the server sends back an IP address, subnet mask, default gateway,
            DNS server, other information to automatically configure itself on
            the network
        - no static configuration
        - valuable when connecting to other networks

## Domain Name System (DNS)

- allows us to use simple names to communicate with devices on the internet
- every device on the internet gets an IP address
- search for a server by its name -> the DNS server will give you the IP for
    that server
- server's IP must be public in order to communicate with it!

## Network Time Protocol (NTP)

- use and NTP server on the network to automatically configure all time times
    on our clients to be exactly the same
- coordinated universal time (UTC)


## Network Management (Telnav and SSH)

- **Telnet** - clear text
    - port number: **23**
- **SSH** (serure shell) - encrypted
    - port number: **22**
    - access devices remotely
    - mechanism to encrypt FTP traffic

- *Putty* -> SSH and Telnet client

## Simple Network Managemen Protocol (SNMP)

- uses an SNMP server to collect information from SNMP clients/agents

- "Walk the tree" -> get all the information about SNMP from all clients
    - browse to the SNMP server and view graphs and statistics about the
        performance of the devices on the network

- SNMP Trap

## Remote Desktop Protocol (RDP)

- remotely manage another device by using it's IP
- port number: **3389**


## Audio/Visual Protocols

- **H.323**
    - port number: **1720**
    - audio/visual mostly used for video conferencing
    - connects monitors and cameras together

- **SIP** - Session Initiation Protocol
    - voice over IP communications in a network- set up voice call between the
        phone and the server, server and telephone company
    - port numbers: **5060/5061**
