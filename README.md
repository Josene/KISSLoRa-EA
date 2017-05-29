##Introduction
This repository has been made to make the code for the Josuino/KISS LoRa publically available.
The code within contains two folders; the libraries used, and an example file. 

##Library usage
Copy both folders in /Libraries to (USER FOLDER)\Arduino\Libraries.
First, we need to enable the PM sensor class, then enable the physical PM sensor.
```
#include <IntemoPM.H>

#define joseneAddress 0x4E

JosenePM JosenePM;

void setup()
{
  Serial.begin(9600);

  JosenePM.begin(joseneAddress, 1);
}
```
JosenePM.begin(uint8_t address, uint8_t channel) sends a 'initialization' command to the sensor, setting it up to allow reading data.
Then, we neet to turn on the PM sensor.
```
...
  JosenePM.begin(joseneAddress, 1);
  JosenePM.powerOn();
}
```
JosenePM.powerOn() turns on the sensor, allowing it to physically read the incoming particles. To retrieve the data, we use the following method:
```
...
void loop()
{
  uint16_t *data = JosenePM.getData(false);
  Serial.print("Josene PM Data:\nPM10: ");
  Serial.println(data[0]);
  Serial.print("PM2.5: ");
  Serial.println(data[1]);
}
```
JosenePM.getData(boolean debug) reads the data from the device, and stores it in an array with a length of two unsigned, sixteen bit integers. The first element in the array is the PM10 value, the second element in the array is the PM2.5 value.
