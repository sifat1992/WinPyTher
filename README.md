## Introduction
The FLIR A400 is an advanced fixed-mount thermal camera intended for automation, research, and industrial monitoring. It offers flexible integration with external systems, real-time streaming via GigE/RTSP, and high-resolution infrared imaging. The A400 is perfect for tasks like condition monitoring, thermal inspection, process control, and research experiments because it is designed for continuous operation and network connectivity, unlike handheld thermal cameras.

This repository details a useful procedure for setting up the FLIR A400 on ROS2 (Linux/WSL2) and Windows (using FFmpeg). It covers ROS2 integration, dataset capture, live video streaming, and installation. The objective is to offer a practical, step-by-step manual, bridging the gap left by the paucity of official documentation and internet blogs.

Note: There aren't many excellent blogs or videos available, and FLIR's documentation is disjointed, or it could be I did not find them. These are the actions that I found to be effective.

## Softwares
The first thing I started to work with was installing Spinnaker SDK from Teledyne's website which provides the actual driver + API libraries + Python bindings. SpinView is the name of the the GUI application and it comes with the SDK installer as an optional component. It’s basically a quick way to view streams and tweak camera settings without coding. 

https://www.teledynevisionsolutions.com/products/spinnaker-sdk/?model=Spinnaker%20SDK&vertical=machine%20vision&segment=iis

After running the installer, SDK+Drivers are always default, but checking the Spinview, PySpin (Python bindings) and GUI is recommended. After finishing the installation, laptop or pc should be booted. Now, spinView should appear in the Start Menu---> fLIR systems and the camera should appear in Device Manager. 

If you have all the cables and componenets of the FLIR camera set up tools or starter kits, then you are golden. However, I only got the FLIR a400 itself and M12 to RJ45 Adapter. To make it work with my laptop, I had to order some cables. 
1.	POE: Gigabit PoE+ Injector 30W IEEE802.3at/af Compliant, Supplies PoE(15.4W) or PoE+(30W) Power Over Ethernet Distances Up to 328ft, PoE Injector Adapter for Camera/Access Point/IP Phones
2.	NETGEAR 5-Port Gigabit Ethernet Unmanaged Essentials Switch (GS305P) - Home Network Hub, Office Ethernet Splitter, Plug-and-Play, Silent Operation.
3.	X-Code-RJ45-Industrial-Shielded-Ethernet M12 8 Pin X-Code Male to RJ45 Cat6a Ethernet Shielded Cable for Cognex Industrial Camera Flexible 3.3Ft|1M
4. UGREEN USB to Ethernet Adapter, 1000Mbps Plug and Play Ethernet Adapter with USB 3.0, Driver Free, RJ45 LAN Network Dongle Compatible with Nintendo Switch, Laptop, PC, MacBook, Windows, macOS, Linux

## Hardware Set Up
Laptop--> UGREEN USB to Ethernet Adapter--> Cat6 cable-->NETGEAR 5-Port Gigabit Ethernet Switch (GS305P)
Flir A400--> NETGEAR 5-Port Gigabit Ethernet Switch (GS305P). 
Camera has blue light blinking and the green light, also on Gigabit Ethernet Switch (GS305P), the used ports will have green lights on that means the camera is working with ethernet properly. 

## Making the camera talk to my laotop:
1. Find camera IP address:
             Win + R --> type "cmd" --> Enter --> ipconfig
Note your IPv4 address (e.g., 192.168.1.50) under "Ethernet adapter." This is the Ethernet network's IP address for your laptop. For streaming to function, the FLIR A400 camera needs to be configured to a compatible address (same subnet, such as 192.168.1.100). IPv4 is what most GigE/RTSP devices (like the FLIR A400) expect.

2. Install FLIR IPConfig 3.5. After Instalaltion it should show the c
