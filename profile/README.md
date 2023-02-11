# Monitoring CO2

**This organisation regroups all codes used in the Monitoring CO2 project, from the microcontroller to the backend, as well as the PCB and 3D models.**

![Main image](https://raw.githubusercontent.com/Monitoring-CO2/.github/main/images/Full_front.jpg)

## [Presentation video](https://www.youtube.com/watch?v=M2izvQClWJk)

Watch the presentation video [here](https://www.youtube.com/watch?v=M2izvQClWJk) (in French).

## Software

- **[Arduino-full](https://github.com/Monitoring-CO2/Arduino-full)** : Full sensor microcontroller program
- **[Backend-server](https://github.com/Monitoring-CO2/Backend-server)** : Backend Web server
- **[Server-Docker](https://github.com/Monitoring-CO2/Server-Docker)** : Docker compose for the backend Web server

## Hardware

- **[PCB]()** : Schematic for the sensor's PCB
- **[3D-modules](https://github.com/Monitoring-CO2/3D-modules)** : All 3D models for the sensor

## Full system diagram

![Diagram](https://raw.githubusercontent.com/Monitoring-CO2/.github/main/images/Full_diagram.png)

## How to set up the project's backend

In order to set up the Monitoring CO2's backend, please read the [deploy guide](https://github.com/Monitoring-CO2/Server-Docker#how-to-deploy).

## Payload format

*Feel free to change the payload format in the [LORA_Module.cpp](https://github.com/Monitoring-CO2/Arduino-full/blob/main/src/LORA_Module.cpp) and [PayloadDecoder.java](https://github.com/Monitoring-CO2/Backend-server/blob/main/src/main/java/fr/polytech/monitoringco2server/LoRa/PayloadDecoder.java) files.*

Currently, the payload is encrypted/decrypted as following :

![Payload](https://raw.githubusercontent.com/Monitoring-CO2/.github/main/images/payload.jpg)

It consists of two bytes of "header" and N\*8 bytes for all messages.

### Header

- The first byte indicates the number of messages that are sent  
  This is a two bytes unsigned short
- The second byte indicates the battery voltage at the time of the upload  
  This is equal to (current_battery_voltage - 2.5) * 100  
  For example 4.15V battery will send 0xA5
  
### Messages

- The first 4 bytes consists of the message timestamp in the Unix format in seconds [example](https://www.epochconverter.com/)
- The temperature is sent as the following : (current_temperature + 25) * 10
- The humidity is sent as the following : current_humidity
- The CO2 is sent as the following : current_co2 / 10
- The motion is sent as the following : current_motion_prob * 15
