
# Modbus - TCP setup

I added yet another protocol to run my home,
the power meters are used for wallbox power consumtion.

## Setup


Components
- multiple SDM630Modbus  V2  Power Meter  https://www.eastroneurope.com/products/view/sdm630modbus
- USR DR-302  RS485 to Ethernet Adapter  https://www.pusr.com/products/din-rail-rs485-serial-to-ethernet-converter-usr-dr302.html
- PoE Power Splitter 12V with IEEE802.3af
- Adapter for barrel jack 5.5 / 2.1mm
- Wago clamps for splitting the Modbus for each device (3 wires)

![IMG_20230901_153519](https://github.com/Dr-schobi/modbus-tcp-power-meter/assets/78444256/a2b23bfa-fa4b-4b76-abb2-2561af4f6d00)



## Configuration

SDM630Modbus
- 38.4kbaud
- addresses 1, 2, 3


Find USR device and assign local IP Adress with USR M0 tool https://www.pusr.com/support/downloads/
then proceed on IP interface

USR DR-302 Settings
- 38.4kbaud
- TCP Server, local port 502
- Expand Fuction > Modbus TCP


## Software

for testing the free Modpoll Windows software seems to work well https://www.modbusdriver.com/modpoll.html

Modbus register numbers can be found in the documentation https://bg-etech.de/download/manual/SDM630-Modbus-V2.pdf


Examples:

check if the device is online at all
> ping [IP]

read floating-point number of the current line frequency of device on modbus address 3
> modpoll.exe -p 502 -a 3 -r 71 -f -t 3:float  [IP]

read total kWh
> modpoll.exe -p 502 -a 3 -r 343 -f -t 3:float  [IP]

read Phase 1 voltage 
> modpoll.exe -p 502 -a 3 -r 1 -f -t 3:float  [IP]




