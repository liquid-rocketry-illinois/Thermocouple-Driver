# Thermocouple Driver
## Introduction

[Documentation](https://docs.google.com/document/d/1IdZL0B9oxNFQynoBRE8_2E1hHAcaAazBmNdDDNkI2ww/edit?tab=t.0) <br/>
The current implementation of the thermocouple driver is built to support I2C communication with the MCP9600 (Microchip) board. The MCP9600 converts thermocouple EMF to degree Celsius with integrated cold-junction compensation. The temperature correction coefficients are derived from the National Institute of Standards and Technology (NIST) [ITS-90 Thermocouple Database](https://data.nist.gov/pdr/lps/ECBCC1C1302A2ED9E04306570681B10748). The MCP9600 corrects the thermocouple nonlinear error characteristics of eight thermocouple types and outputs ±0.5°C/±1.5°C (Typ./Max.). <br/>

## Usage
<img width="480" height="360" alt="thermocouple_driver_wiring" src="https://github.com/user-attachments/assets/3910a3c8-b975-40a0-b8a2-617fb01989d9"/> <br/>
The connections to be made between the STM32H753ZI Nucleo-144 and MCP960 are to be made as follows: <br/>
<table border="1" style="border-collapse: collapse;">
   <thead>
       <tr>
           <th>MCP9600</th>
           <th>STM32H753ZI</th>
       </tr>
   </thead>
   <tbody>
       <tr>
           <td>VIN</td>
           <td>3.3V</td>
       </tr>
       <tr>
           <td>GND</td>
           <td>GND</td>
       </tr>
       <tr>
           <td>SCL</td>
           <td>PB6, TX</td>
       </tr>
       <tr>
           <td>SDA</td>
           <td>PB7, RX</td>
       </tr>
       <tr>
           <td>ADR</td>
           <td>GND</td>
       </tr>
       <tr>
           <td>A[3:0]</td>
           <td>NC</td>
       </tr>
   </tbody>
</table>
<i>ADR is routed to GND to force an address value of 0x60. It may be configured differently to set a different address value.</i> <br/>

**A thermocouple is connected to the MCP9600 as follows**: <br/>
🔵 BLUE wire to positive channel (+) <br/>
🔴 RED to negative channel (–) <br/>

## Main Parts
**MCP9600 Thermocouple Amplifier**: [Adafruit MCP9600 Breakout Board](https://www.adafruit.com/product/4101), [MCP9600 IC](https://www.digikey.com/en/products/detail/microchip-technology/MCP9600-E-MX/6009305?gclid=26fb766dc0161d939b531fa5d559c2f0&gclsrc=3p.ds&msclkid=26fb766dc0161d939b531fa5d559c2f0) <br/>
**TCA9548A 1-to-8 Multiplexer**: [Adafruit TCA9548A Breakout Board](https://learn.adafruit.com/adafruit-tca9548a-1-to-8-i2c-multiplexer-breakout/overview), [TCA9548A IC](https://www.digikey.com/en/products/detail/texas-instruments/tca9548apwr/3615458?_gl=1*1p3cjpq*_up*MQ..&gclid=26fb766dc0161d939b531fa5d559c2f0&gclsrc=3p.ds) <br/>

## Specifications
**Operating voltage range**: 2.7–5.5 V <br/>
**Absolute maximum voltage range**: 6.0 V <br/>
**Storage temperature**: -65°C to +150°C <br/>
**Ambient temperature with power applied**: -40°C to +125°C <br/>
**Sensor accuracy**: (see [MCP9600 datasheet](https://ww1.microchip.com/downloads/en/DeviceDoc/MCP960X-Data-Sheet-20005426.pdf), pg. 3 MCP9600/01) <br/>
**Thermocouple support for**: K-, J-, N-, T-, S-, R-, E-, B-type thermocouple <br/>

## Compiling

[placeholder]

## Reference

The driver is written with respect to the STM32H753ZIT6. With respect to the .ioc file, all references are to the STM32H7 HAL and configured according to the STM3253ZIT6 pinout. The h7zit.ioc file currently enables two multimedia peripherals: I2C1 (PB6/TX, PB7/RX) and USART3 (PD8, PD9).
