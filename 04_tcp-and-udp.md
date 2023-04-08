# Transport layer protocols

 - **TCP** - Transmission Control Protocol
 - **UDP** - User Datagram Protocol


## Transmission Control Protocol (TCP)

- transfer website from server to client -> a **session** must be established
    between the client and the server
    - **session** -> mechanism "i have to get some data from you so we're going
        to have to set up this specialized communication session"

- establishing communication:
    - e.g. Homer calling Marge steps:
        - pick telephone
        - wait for dial tone
        - dial phone number
        - wait for phone to ring
        - wait for Marge to pick up phone
        - Marge answers and says "hello"
        - Homer says "hello" -> *established communication session*
        - throughout the conversation, both Homer and Marge are giving clues
            as to whether or not they received the message from the other party
        - if they don't get the message (or parts of the message) -> Homer/Marge
            say "i don't understand", "you're breaking up" -> "repeat what you
            just said"
    - ways in our session of letting the other person know we didn't get the
        information they sent
- protocol for ending the session - mechanisms to end the session between the 2
    parties and prevent future communications
    - they can be:
        - nice: "goodbye" followed by hanging up the telephone
        - abrupt: hanging phone without saying goodbye

- conclusion:
    - specialized process to establish the session between 2 people talking on
        the phone
    - ways in the conversation of acknowledging that the info was received or
        that information was not received
    - ways of tearing down the session (polite/abrupt)


### The 3-way handshake (for TCP)

- **SYN -> SYN-ACK -> ACK**

- "client" <--> network <--> "server"

- once we know the IP address of the web server -> 3 steps to establish the
    connection between client and server:
    - client sends a **SYN**(synchronized message) to the server
        - state -> *SYN sent*
    - server sends back a reply **SYN-ACK**(acknowledgement of synchronization)
        - state -> *SYN Received*
    - client sends **ACK**(acknowledgement) to the server
        - state -> *Session Established*

- once we have the 3-way handshake established -> layer 4 protocol is complete
    - we can use an application layer protocol(HTTP or HTTPS) to communicate
    with the server
        - e.g. client sends message "hey, give me the website" server "here's
            the website"

- layer 4 -> establish a session
- layer 7 -> transfer the website itself

- during this conversation, if the entire website did not get sent to the client
    - the client can send a message back to the server -> "hey I'm missing info"
    - if the server doesn't get the entire request from the client -> "send me
        more information, i didn't get that last message"

- way of navigating the conversation to say "yes, I've heard what you said" or
    "no, i didn't hear what you said"


### The 4-way Disconnect (for TCP)

- **FIN -> FIN-ACK -> FIN -> FIN-ACK**
    - device A sends **FIN**(Finish message)
        - state -> *FIN-WAIT*
    - device B sends **FIN-ACK**(Finish message acknowledged)
    - device B sends **FIN** message to device A
    - device A sends **FIN-ACK** to device B
        - state -> *CLOSED*

- quickly end a session: **RST** (TCP Reset)
    - just like hanging up a phone
    - "conversation is not right, something's wrong"
    - firewall may decide that the conversation is not good and shut it down

- conclusion:    
    - TCP is a very reliable protocol
        - has mechanisms built in to verify that the data sent was received
        - has a message of setting up a session between the endpoints
        - has a nice way of ending the session


## User Datagram Protocol (UDP)

- works similar with walkie-talkies (maybe address it to a certain person)
    - e.g. "Hey, I need some info from Bill" and hopefully Bill will respond

- wrap up some application layer message (e.g. DNS) -> "Hey, send me the data!"
    - server responds by sending the data -> "Hey, here's the data"

- no 3-way handshake
- no reliable communication -> message sent may or may not be received by the
    server -> we may have no way of knowing that
- no sequence numbers and no acknowledgement numbers
    - those are used by **TCP** to verify that the data sent was received
- used for efficient data transfers

- DNS (Domain Name System) -> it's used to resolve a host name (e.g. google.com)
    into a usable IP address that can be put into an IP packed header
    - the value of **UDP** here is that for a protocol like DNS, it's just a
        simple message that we send to the server -> "Hey DNS server, what's
        the IP address of google.com" -> server responds with the IP address
        - no need for SYN->SYN-ACK->ACK, send message to server and then
            FIN->FIN-ACK->FIN->FIN-ACK

## Transport Layer Addressing: Port numbers

- at the transport layer, we are using port numbers to identify (tipically) an
    application layer protocol that's being used
- in TCP or UDP there are always a *source port number* and a *destination port
    number* in our segment header
    - categorized into different areas:
        - **Server Port Numbers**
            - *well known*: 0 -> 1023
                - e.g.: HTTP(80), HTTPs(443), FTP(20,21), SSH(22), Telnet(23)
            - *registered port numbers*: 1024 -> 49151
                - custom applications (official or unofficial port numbers)
                - proprietary (e.g. IBM, H.323, SIP have protocols, RADIUS
                    protocol for authentication has a port number here, )
        - **Client Port Numbers**
            - *ephemeral port numbers* (temporary): 49152 -> 65535

- typically, we're gonna see **well-known** port numbers used as our
    *destination* port number when we're communicating with the server

- when using transport layer protocols (for TCP)
    - *source port* -> is going to come from the *client* (ephemeral range)
    - *destination port* -> whatever service we're trying to access on the
        destination device

- **TCP header** (segment header) -> contains source and destination port number
    - e.g. client -> network -> server
        - TCP header:
            - source port number -> ephemeral (49152 -> 65535)
            - destination port number -> e.g. Telnet (23)

## Application Layer Protocol Dependency

- **TCP**:
    - HTTP, HTTPs, FTP, SFTP, SMB, POP3, IMAP, SMTP, LDAPs
    - Telnet, SSH, RDP
- **TCP/UDP**:
    - LDAP
    - DNS, SIP, H.323, SNMP
- **UDP**:
    - TFTP
    - DHCP, NTP

- all protocols are going to use **IP** at the network layer !
