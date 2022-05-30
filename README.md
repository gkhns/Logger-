
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

This link is from the Wireshark.org: 

https://wiki.wireshark.org/USB

Here are the steps:

1) Apply filter: `((usb.transfer_type == 0x01) && (frame.len == 35)) && !(usb.capdata == 00:00:00:00:00:00:00:00)`

    `(usb.transfer_type == 0x01)`: To list all interrupt communication
    
    `(frame.len == 35)` : To include frame lengths equal to 35
    
    `!(usb.capdata == 00:00:00:00:00:00:00:00` : To exclude empty HID data
    
2) Add HID data as a new colum
3) Export data as a CSV file 
4) Trim data: `cat exported.csv | cut -d "," -f 7 | cut -d "\"" -f 2 | grep -vE "HID Data" > hexa.txt`
5) Modify python code originally presented in https://abawazeeer.medium.com/kaizen-ctf-2018-reverse-engineer-usb-keystrok-from-pcap-file-2412351679f4

    https://github.com/gkhns/Logger-/blob/main/code.py


The code can't understand whether the CAPS LOCK was on or off but it gives indicators when there is a change. There is a little bit more work to do to get the final answer. 


