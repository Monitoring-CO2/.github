# Monitoring CO2

Build in progress...

## Payload format

*Feel free to change the payload format in the [LORA_Module.cpp](https://github.com/Monitoring-CO2/Arduino-full/blob/main/src/LORA_Module.cpp) and [PayloadDecoder.java](https://github.com/Monitoring-CO2/Backend-server/blob/main/src/main/java/fr/polytech/monitoringco2server/LoRa/PayloadDecoder.java) files.*

Currently, the payload is encrypted/decrypted as following :

![Payload](https://raw.githubusercontent.com/Monitoring-CO2/.github/main/images/payload.jpg)

It consists of two bytes of "header" and N*8 messages.

### Header

- The first byte indicates the number of messages that are sent  
  This is a two bytes unsigned short
- The second byte indicates the battery voltage at the time of the upload  
  This is equal to (current_battery_voltage - 2.5) * 100  
  For example 4.15V battery will send 0xA5
  
### Message

- The first 4 bytes consists of the current timestamp in the Unix format in seconds [example](https://www.epochconverter.com/)
- The temperature is sent as the following : (current_temperature + 25) * 10 °C
- The humidity is sent as the following : current_humidity
- The CO2 is sent as the following : current_co2 / 10
- The motion is sent as the following : current_motion_prob * 15
