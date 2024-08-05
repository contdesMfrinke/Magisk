
 
In our case it was even more complicated, because our platform was a real time system, so we could not use dlls made based on some other open source code (non LV). Even worse, in the end we had to totally abandon the Ethernet interface because there was even no company who could provide us a solution (we had a special configuration of a Siemens PLC, where we had a separate Ethernet card, and somehow non of the available apps were able to establish communication...).
 
I started to work on this project again with labview and s7-1200.I am purely new to this plc and i need to know the basic hardware configuration that are required in this communication.With my basic R&D i wanted to use modbus tcp protocol for this communication.I even tried with building shared variables according with help of this forum. But i was unsuccessful as it was showing some errors.
 
**Download File ✓✓✓ [https://amreamate.blogspot.com/?d=2A0SVv](https://amreamate.blogspot.com/?d=2A0SVv)**


 
I have not worked with the S7-1200 but from the manual it supports UDP and TCP/IP connections. I would use a UDP to communicate between your labview vi and the PLC. Set up a send and receive. Insure to add spare words so you do not have to change data sizes for future.
 
Nothing special, TIA is a master of troubles and issues. First, make a correct settings for your PC ethernet NIC, make the IPv4 to be in the same subnet, for example 192.168.0.150. Then plug the cable from your PC to PLC, choose PN/IE, select the NIC you want to use (those that you configured a static IPv4), direct slot x1, start search.
 
What does your layer 2 (Ethernet) network connectivity look like? Just a direct cable? (Does straight / crossover matter?) Or are you running this through a switch? If so, what sort? Dumb, or managed? If managed, does the switch know anything about IP multicasting = does it support IGMP Snooping?
 
Not sure if this was the TIA portal or some other Siemens PLC config software (of the Simatic stable), but once upon a time I've witnessed a problem where some such management software could not find the Profinet devices it was supposed to configure/manage. Ping did work, Profinet IO payload sessions did work, but device detection in the "studio" did not.
 
Wireshark disclosed that the "studio" software on the PC was using multicast destination addresses (possibly L2 multicast, not necessarily L3 multicast, I don't remember anymore) and the packets to multicast destination did not pass through the switch (got dropped / filtered by the switch).

From there, it turned out that the switch had IGMP snooping enabled (user configurable option of the switch management firmware) and apparently the Siemens Profinet devices do not run IGMP, so the switch did not know about any multicast recipients (who would've subscribed via IGMP), and therefore did not open any port to multicast traffic.
 
If you have this kind of "simple multicast traffic pattern without IGMP", you need to disable IGMP snooping in your switch. As a result, the switch will effectively broadcast any traffic with a multicast destination address. This is also what dumb (unmanaged) switches apparently default to.
 
Not sure how TIA Portal works with the network stack on the PC where it runs. I mean - at the device detection stage. It possibly uses a raw socket to send L2 multicast, or it may have a filter driver installed to do this in the kernel space. No idea. I mean to say that you should try disabling the Windows firewall, just speculatively, to see if that makes a difference.
 
Even if you do not want to install and run Wireshark on the PC with TIA portal (Wireshark installs another filter driver for the packet capture, I believe - which might clash with TIA portal, not sure, I've never tried) , you can always plug in another computer running some sniffer (Wireshark et al) into the same switch, and if you can see the multicasts coming, you know that this is not your problem. Unfortunately, through a switch, you won't see any unicast responses from the devices responding to the multicast detection probe... for that you'd need a mirror port on the switch, or a hub (cough) or a device called the passive tap.
 
There is no official way from Siemens to communicate with S7-PLCSIM V13-15, so we scan the running processes, and read and write directly to the PLCSIM process memory. That is why we provide project templates with a special FC to run in the simulator.
 
Using NetToPLCSim: In the past, we were able to successfully use NetToPLCSim to expose the simulated PLC from S7-PLCSIM to the network, and then connect Factory IO to it through the S7-1200/1500 driver.
However, we did have both applications running on the same computer, but we believe it would also work on a different PC.
 
Using S7-PLCSIM Advanced: S7-PLCSIM Advanced exposes the simulated PLC to the network without having to use external applications. You can find the manual for S7-PLCSIM Advanced here. I think pages 17, 18 and 19 may help you create a distributed instance.
After this, you can follow our tutorial to set up S1200/S1500 (instead of a real PLC, you use the simulated one).
 
Fortunately, Siemens offers the SIMATIC Automation Tool as a free download (just sign up for an account first) on their website. The SIMATIC Automation Tool was perfect for our client's situation. It allowed them to seamlessly download the updated PLC code and commission the machine on schedule.
 
First, you will learn how to connect a computer to the same network as the PLC. I will then show you how to save the PLC program in a format that the SIMATIC Automation Tool can use. Next, I will walk through using the SIMATIC Automation Tool itself. Finally, I'll review some of the other capabilities of the SIMATIC Automation Tool.
 
In order to download to a PLC using the SIMATIC Automation Tool, you need the PLC program in an S7S File Format. Whoever wrote the PLC program should follow these steps using TIA Portal to generate the S7S File for you to use.
 
First, map a file directory on the TIA Portal computer to a **Card Reader/USB Memory** location. To do this, open the PLC project in TIA Portal and click **Project -> Card Reader/USB Memory -> Add user-defined Card Reader**:
 
I have a problem between my plc and robot. I have a siemens plc s1500 and a fanuc robot, im trying to comunicate them with ethernet ip. I have follow all the steps but i cant comunicate the plc with the robot, both of them are in the same ip range and i can ping each one from the computer. Also i can ping the plc from the robot. The plc is the scanner and the robot is the adapter
 
In the Fanuc robot, the ethernet ip connection is online but not running. I have checked all the EDS data from the robot and i am sending thease values correctly from the plc. Also the tcp/ip connection has been initialized.
 
I have a 1517TF-3 plc with v2.0 firmware, im using tia portal v15.1 and the robot controller is Fanuc R-30iB Plus. Im trying to communicate the plc with the robot using ethernet ip. In Tia portal im using LCCF enetScanner block, the plc works as scanner and the robot as adapter. Im sending to the robot the IP address, vendor identifier, product type,...
 
The robot is configured to work in rack 89 and slot 1, also it has the ip address and it communicates with the plc. But in the plc the scanner active signal is always off. The ethernet ip connection is activated and the status is online, but is not running, im using the first connection.
 
May I ask, where you get the "RPI >= 32 ms" from? I am currently configurating a Fanuc Siemens connection with this function block and did not find this value in any of the manuals. Is this something you have found out by experiments?
 
RPI for PLC side. Use "packetinterval" parameter of Function block. You can found parameter in instance DB of FB. If you using RPI less than 32 connection problems occured randomly. Because Siemens PLC is not powerfull CPU for Ethernet/IP
 
S7-1500 manages to support EIP Communication, S7-1200 does not have enough power (communicates but when loading a new configuration in the PLC, the communication drops). For me, the main problem was the incorrect configuration of the input and output registers on both sides (Robot and PLC). In the robot, the registers are 16 bits, while in the S7 they are 8 bits.
 
The CP5512 card and the PC Adapter can communicate on either an MPI or PROFIBUS port. Note that PROFIBUS is labeled as DP on the Siemens connection ports. These cables can piggyback on existing connectors. Be aware that the PC Adapter draws its power to work from the connection port so check the power LED for proper operation. The CP5512 card draws its power from the computer.
 
For the PC Adapter click on the Properties button and make sure the Station Parameters Address is a unique network address. It should not conflict with existing PLC and slave devices on the network. Also, check under the Local Connection tab and make sure connection selection matches the port the cable is connected into.
 
Once the proper interface is selected and the properties are set then click OK and use the Accessible Nodes window to check for successful communications. It should work. If not double-check the connection and cable. With the CP5512 and PC Adapter cables, you should use the MPI port, as this is the default connection for Siemens.
 
Partial downloads are used in existing projects where only one or more blocks will be downloaded. To perform this type of download select the block(s) you wish to download and then select the PLC > Download menu item or the download button .
 
Holding down the Ctrl key or the Shift key allows more then one block to be selected at a time. Be careful though as the order of download will occur in the order that the blocks were selected. This may mean that an error will occur if a block is called before it is downloaded.
 
The CPU