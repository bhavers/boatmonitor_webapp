# boatmonitor
Monitoring battery status and location of my boat. This repository contains the server side of the solution, running on IBM Bluemix.
The project uses a Sodaq One Arduino board and a simple additional circuit to capture the data. The Sodaq One board uses GPS to capture position and report the battery voltage (3 - 4.5V) and temperature  of the Sodaq One board. An additional circuit is used to measure the battery voltage (12-15V) and battery temperature of my two batteries on the boat. The circuit has 2 voltage inputs and 4 temperature inputs (2 for the batteries, 1 for the environment, 1 for the fridge).    
The standard Sodaq tracker Arduino code is used as a base and is extended for the additional sensors. The Sodaq One board has a LoRaWAN interface which is used to send data to the The Things Network (TTN).
The Things Network publishes the sensor data on  a MQTT topic.

This is where the code of this repository starts.
In Bluemix a Nodered flow is configured that listens for the MQTT topic and stores the sensor data in Cloudant.
On Cloudant two views will list a summary of all sensors and the history of data.
Another Nodered flow defines two API that are publicly available to listen query the data in Cloudant. 
A HTML5 application will display the information (using d3.js for visualizing graphs).
