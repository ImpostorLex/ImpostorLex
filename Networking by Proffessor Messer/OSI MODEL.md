# OSI MODEL

- stands for Open Systems Interconnection Reference Model

- Is a model or a guide on how data move across the network

- Have 7 different layers (All People Seem To Need Data Processing)
	- Layer 7: [[Application Layer]]
	- Layer 6: [[Presentation Layer]]
	- Layer 5: [[Session]]
	- Layer 4: [[Transport]]
	- Layer 3: [[Network]]
	- Layer 2: [[Data Link]]
	- Layer 1: [[Physical]]


## PHYSICAL LAYER
- Ability to signal a network from one part of the network
- Signaling, cabling, and connectors
- No protocols

## Data Link Layer
- Where all protocols (Layer 7 to 3 protocols) rest on top
- Also known as Data Link Control protocols or DLC
	- Protocols that run as DLC protocols such as
        - Media Access Control (MAC) on Ethernet
        - Switches make most of their forwarding decision based on what is the MAC address, layer is also known as the 'switching' layer

Example:
Two #network_interface_card and their #MAC_address
![[Pasted image 20220627165442.png]]
Communications between the two using the MAC address can refer to as Layer 2 communication

## Network Layer
- Also known as the 'routing' layer
- Internet Protocol
	- Devices that forwards decisions based on the IP addresses is communicating at Layer 3 (Network Layer)
- #Frames are fragmented or broken down to pieces in order to move those between different types of networks e.g Eth1. > WAN > Eth2

## Transport Layer
- Also known as "post office" layer because of how the data is being delivered and where is the data being delivered
- Protocol used Transmission Control Protocol and User Datagram Protocol
- Used when accessing a page, most of the time webpage are large that sending in one frame is not possible, frames are chopped into pieces then send across the network and put back together on the other side

## Session Layer
- Is a communication management layer between devices that starts, stop, restart communicatin between devices
- Control protocols (TCP) and Tunneling protocols (VPN - securely send and receive data between two networks)

## Presentation Layer
- Often combined to application layer
- Character encoding - the layer takes the data and put it in a form that we can understand
- Application encryption

## Application Layer
- What we see, for example Google.com we will see Google.com 
- Protocols
	- *FTP* - File transfer protocols
	- *DNS* - Domain Name System / 8.8.8.8 (for computers), Google.com (for humans)
	- *HTTP/HTTPS* - Browsing through the web with HTTP or HTTPS (much secure)
	- *POP3* - Commonly used for receiving emails over the internet


## OSI  In the real world
![[Pasted image 20220628111913.png]]
There are 2005 bytes captured on Physical Layer, there is MAC address for source and destination devices in Data Link Layer, we have the IP address of the source and destination in the Network Layer,  is a connection oriented protocol TCP for the network layer, and Layer 5, and 6 is implemented in the app layer 

![[Pasted image 20220628112501.png]]

