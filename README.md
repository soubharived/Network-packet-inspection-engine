

/----------Requirements---------/


g++ (GCC) 15.x.x

/---------------Compile the Project-----------/

g++ -std=c++17 -O2 -I include -o dpi_simple src/main_working.cpp src/pcap_reader.cpp src/packet_parser.cpp src/sni_extractor.cpp src/types.cpp

/----------Run the Program-----------/
.\dpi_simple test_dpi.pcap output.pcap

/-------------What the Program Does Internally----------------/
For every packet the engine performs the following steps:

Read packet from PCAP
↓
Parse Ethernet header
↓
Parse IP header
↓
Parse TCP/UDP header
↓
Extract packet payload
↓
Detect TLS Client Hello
↓
Extract SNI (domain name)
↓
Identify application
↓
Apply filtering rules
↓
Forward or drop packet

/-----------Example Output Explanation----------------/

Example output:

Total Packets: 77
Forwarded: 77
Dropped: 0
Active Flows: 43

Meaning:

Field	          Explanation
Total Packets	  packets read from PCAP
Forwarded	      packets allowed
Dropped	packets   blocked
Active Flows	  number of network connections


/------------What is a Flow?-------------/

A network connection is identified by a 5-tuple:

Source IP
Destination IP
Source Port
Destination Port
Protocol

Example:

192.168.1.10:50000 → 142.250.182.206:443

Packets with the same 5-tuple belong to the same flow.
