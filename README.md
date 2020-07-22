# ESPhome engine coolant and oil pressure sensor
 This project uses ESPhome to make engine Coolant and Oil pressure sensors using ESP8266 and an ADS1115 16-bit A/D converter.
 This is a companion circuit to go with my RealDash MQTT to CAN bus Node-red 2-way project. https://github.com/sdc53/RealDash-CAN-MQTT-Node-Red-2-way

## Why I'm doing this
I have a classic vehicle that does not have OBD-II or an ECU, and I want to moderize my dashboard using a tablet. I needed a way to easily and reliably convert sensor data from analog to digital, and be able to add additional sensors over time.  I am using these sensors to communicate with RealDash over MQTT.
 
## Benefits
* No programming needed, only editing the ESPhome YAML config file is needed
* Wireless over-the-air updates
* Very accurate A/D conversion using reference voltage and 16-bit A/D converter
* Talks over MQTT and updates coolant temp and oil pressure once a second (configurable)
* Relays retain existing analog gauge function (fail-safe), works with one-wire senders that ground thru chassis

## Circuit picture
![Breadboard](https://github.com/sdc53/ESPhome-engine-coolant-and-oil-pressure-sensor/blob/master/circuit%20picture.jpg)

## Schematic
![Schematic](https://github.com/sdc53/ESPhome-engine-coolant-and-oil-pressure-sensor/blob/master/Schematic_bus%20esp8266%20sensor_2020-07-20_17-23-59.png)

## Video link
Project overview video: https://youtu.be/UH3q9yckc6g
There are other videos on my channel related to this project, including a technical overview of the software and companion github project.

## BOM
This table contains affiliate links, I may receive a small commission if you choose to purchase using them. I obtained data sheets for the senders I already have installed, you will probably want to use your existing senders as well, which will require altering the configuration file. 
| ID | Name                     | Designator | Footprint         | Quantity | Manufacturer Part | Manufacturer | Supplier  | Supplier Part            |
|----|--------------------------|------------|-------------------|----------|-------------------|--------------|-----------|--------------------------|
| 1  | NODEMCU ESP12E ESP8266EX | U1         | ESP12E_DEVKIT-V1B | 1        |                   | Makerfocus   | Amazon    | https://amzn.to/32xisrJ  |
| 2  | 12v-5v buck converter    | U2         |                   | 1        |                   | Chuangruifa  | Amazon    | https://amzn.to/3jiLVvC  |
| 3  | 220                      | R1         | R0201             | 1        |                   | Plusivo      | Amazon    | https://amzn.to/32ymTCw  |
| 4  | 100                      | R4         | R0201             | 1        |                   | Plusivo      | Amazon    | same as above            |
| 5  | 1uf                      | C1,C2      | C0201             | 2        |                   | Plusivo      | Amazon    | https://amzn.to/2WyRQ5H  |
| 6  | Temp sender              | R2         | R3                | 1        | 6835              | Equus        | Orielly's |                          |
| 7  | Pressure sender          | R3         | R3                | 1        | Datcon 240-33     | Maximatecc   | Amazon    | https://amzn.to/30r0jJy  |
| 8  | ADS1115                  | U3         | ADS1115 ADAFRUIT  | 1        |                   | Makerfocus   | Amazon    | https://amzn.to/3fCVfrP  |
| 9  | 5V_Relay_Module_4Ch      | U4         | NODEMCU_V3_ESP12E | 1        |                   | FTCblock     | Amazon    | https://amzn.to/30qN8Il  |
| 10 | Breadboard               | none       |                   | 1        |                   | REXQualis    | Amazon    | https://amzn.to/32wXrgN  |

## Instructions
0. This project and its config files assume you already have ESPhome installed and know how to use it. If you don't, the easiest way to get started is to install Home Assistant on a Raspberry Pi, and install the ESPhome add-on.  There are plenty of tutorials on the internet instructing you how to do this.
1. Build the circuit
2. Load the config file into ESPhome
3. Configure your wifi, SSID, password, and static IP address (or use DHCP)
4. Download and flash the firmware, the first time using a Micro USB cable and ESPhome flasher.  Subsequent updates can happen over wifi.
5. I am driving the temp and oil senders using 5v. Normally they operate using 12v.  This has not been a problem for me, but you'll want to make sure no 12v signals enter the circuit (except where indicated for the power supply) when installing it in your vehicle.
6. I bench tested the unit using an extra coolant temp sender I purchased, and a 100 Ohm placehold resistor for the oil pressure sender before installing it in my vehicle.
7. If you use different senders, you will need to edit the config file for the resistance values, calibration tables, B-values, and so on as appropriate. These values are for my vehicle and senders.
