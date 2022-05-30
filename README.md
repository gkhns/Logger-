
**Challenge Description**

A client reported that a PC might have been infected, as it's running slow. We've collected all the evidence from the suspect workstation, and found a suspicious trace of USB traffic. Can you identify the compromised data?

Given: PCAP file

As the first step, we open the PCAP file in Wireshark:

* Capture File Properties --> Elapsed Time --> 55 seconds
* Protocol Hierarchy --> 100% USB traffic and 18.9% Text Items

Wireshark reveals HID data. HID stands for **Human interface device** 

A human interface device or HID is a type of computer device usually used by humans that takes input from humans and gives output to humans (Reference: https://en.wikipedia.org/wiki/Human_interface_device)


This reference below is very relevant to this challenge: 

https://book.hacktricks.xyz/generic-methodologies-and-resources/basic-forensic-methodology/pcap-inspection/usb-keystrokes
