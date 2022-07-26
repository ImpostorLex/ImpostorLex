
# Network Edge
Applications and hosts.

Hosts has two categories #clients and #servers.

---

## Access Networks
Also known as #edge_router that physically connects end system to the first router.

![[Pasted image 20220702150739.png|center]]

Two types of (common) broadband residential access are *digital subscriber line*(DSL) and cable. 

Obtains Internet on local telephone company (telco) most of telco have also become Internet service providers.

---

### Digital Subscriber Line

 When a customer uses a DSL, that telco is their ISP.
	
Uses existing telephone lines and exchange data with digital subscriber line access multiplexer (DSLAM) located at CO or Central Office.
	
The #DSL modem takes digital data and translates it to high-frequency tones for transmission over telephone wires to the CO
	
Splitter seperates data and telephone signals arriving to home and forwards the data signal to the DSL modem
	
The DSLAM seperates the data and phone signals and sends the data to the internet
	
DSL provider limits residential rate (transmission rate upstream and downstream) different rates available at different prices.
![[Pasted image 20220702151755.png|center]]

---

### Cable Internet Access

#cable_Internet_access uses existing cable television company's existing cable tv infrastructure obtains from company that provides cable tv
	
Fiber optics are used to connect cable head end to the neighboorhood-level to reach invididual houses, both fiber and coaxial cable are used it is often referred as hybrid fiber coax (HFC)
	
Cable internet access uses special modems also known as #cable_modems is an external device that connects to the home PC through the Ethernet port
	
Cable modem termination system (CMTS) turns the analog signal, signal sent from the cable modems in many downstream homes back into digital format divides HFC network into two upstream and downstream

Used to provide high speed data services, such as cable Internet or Voice over Internet Protocol
	
Cable internet access is a shared broadcast medium, every packet sent by the head end travels downstream on every link to every home and every packet sent by home to upstream channel travels to head end.
	
if several users are simultaneously downloading a file on the downstream channel the actual rate will be slower than the considered whole downstream rate.
![[Pasted image 20220703154158.png|center]]
		
  ---

### Fiber To Home
Provides an optical fiber path from CO to the home.
	
Non-metallic they are unaffected of electromagnetic interfererance (i.e weather)
	
*Direct Fibers* one fiber leaves CO and each fiber are shared by many homes until it gets relatively close to the homes then the fiber splits into customer-specific fibers.
	
- Two optical-distribution network architectures that perform the splitting.
	- Active optical networks (AONs) is basically switched Ethernet.		
		
    - Passive optical networks (PONs) each home has a optical network terminator (ONT) which is connected by dedicated optical fiber to a splitter.
            
		- Splitter combines number of homes usally less than 100 onto a single, shared optical fiber which connects to an optical line terminator (OLT) into the CO.
				
			- OLT provides convesation between optical and electrical signals connects the internet via telco router and at home users connect to a home router usually wireless to the Optical Network Terminator and access the Internet via the home router.
				
				- All packets sent from OLT to the splitter are replicated, similar to #cable_head_end.
				- ![[Pasted image 20220705104554.png]]
    
---

### Access in the Enterprise and Home
LAN used to connect an end system to the #edge_router, Ethernet is generally used in corporate, university, and home networks.
	  
Ethernet used a twisted-pair copper wire to connect to a Ethernet switch or network of interconnected switches which then connected into a larger Internet, (Users have 100Mbps to 10Gbps and Servers have 1Gbps to 10Gbps)

![[Pasted image 20220705105513.png|center]]

 Users are accessing the Internet Wirelessly via mobile devices and other 'things' wireless users transmit/receives packets from/to an #access_point that is connected to an enterprise's network (most of the time using wired Ethernet) which connects to the wired Internet (users should be 10-20 meters of the access point).
	  
 Many homes combines broadband residentail access ( #cable_modems or #DSL) to create powerful home networks
 
![[Pasted image 20220705112415.png|center]]

---

### Wide-Area Wireless Access: 3G and LTE 4G and 5G
Iphones and android devices employ the same wireless infrrastructure used for cellular telephony to send/receive packets through a base station that is operated by cellular network provider users need to be 10-20 kilometers of the base station (4G and 5G).

---

## Physical Media

^b5779b

Refers to the physical materials that store and transmit information.

Physical medium is a series of links and routers ( #transmitter-receiver pair) where the packet spreads until it arrives on destination 

Doesn't have to be the same type of transmitter-receiver pair

- Two types of **physical media**: 
	- *Guided media*: guides the waves (from transmitter antenna to receiver antenna) with a strong physical medium
	
	- *Unguided media*: waves spreads in the atmosphere and in the outer space such as in wireless LAN or digital satellite channel
	
- Examples of Physical Media

	- **Twisted-pair copper wire (guided)** 
	
		- the cheapest and most commonly used for guided transmission medium 
		- #DSL users uses twisted pair when the user is close to the ISP's CO.
		
		- it consists of two insulated copper wires, each 1mm thick in arranged in a regular spiral pattern so to reduce electrical interference from similar pairs.
		
		- Usually they are bundled together in a cable wrapping pairs into a protective shield, a wire pair is part of a single communication link.
		
		- ***Unshielded twisted pair*** 
			- commonly used for computer networks for LANs.
			
			- Data rates using LANs is 10 Mbps to 10 Gbps, still depends on the thickness of the wire and distance of sender and receiver.
	 
	- **Coaxial cable (guided)**
		- consists of two copper conductors that the larger covers the smaller.
		
		- Can achieve high data transmission rates.
		
		- Common in cable television system since CTS includes with cable modems to provide residential user access to the Internet.
		
		- In cable television and cable Internet access the transmitter change the digital signal to a specific frequency band and the resulting analog signal is sent from transmitter to one or more receivers.
		
		- End systems can be connected directly to the cable.
		
	- **Multimode fiber optic cable (guided)** 
		- Is a thin flexible medium that conducts pulses of light with each pulse represents a bit.
		
		- Up to tens to hundred gigabits per second.
		
		- Frequent in the backbone of the Internet.
		
	- **Terrestrial radio spectrum** 
		- Carries signals in the electromagnetic spectrum.
		
		- Does not require physical wire.
		- Can penetrate walls.
		
		- Provide connectivity to mobile users.
		- Can potentially carry signals for long distances.
		
		- Propagation Environment can determine path loss and decrease of signal strength as signals travel far and travels through objects.
		
		- Multipath fading where due to signal reflection off interfering objects and transmissions of other electromagnetic signals.
	
	- **Satellite radio spectrum**
		- Links two or more Earth-based microwave #transmitter-receivers.
		
		- Receives transmissions on one frequency band, reconstruct the signal using a repeater and transmits the signal on another frequency.
		
		- Two types of satellites:
			- **Geostationary satellites** 
				- Stays on the same spot forever, 36,000 kilometers above Earth's surface.
				
				- #Propagation_delay of 280 miliseconds.
				
				- often used without access to #DSL or #cable_Internet_access 
			
			- **Low-earth orbiting satellites** 
				- Rotates around and placed much closer to Earth.
				
				- Can communicate with each other and with transmitter-receiver pairs
				
				- Many LEO are deployed to continue coverage in a area.
			
---

Continues at [[NET Network Core|Network Core]].
Map of [[Networing MOC|Content]].