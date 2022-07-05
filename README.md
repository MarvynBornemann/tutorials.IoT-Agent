# Digital Twin of SmartWorld by FIWARE [<img src="https://img.shields.io/badge/NGSI-LD-d6604d.svg" width="90"  align="left" />](https://www.etsi.org/deliver/etsi_gs/CIM/001_099/009/01.04.01_60/gs_cim009v010401p.pdf)[<img src="https://fiware.github.io/tutorials.IoT-Agent/img/fiware.png" align="left" width="162">](https://www.fiware.org/)<br/>

[![FIWARE IoT Agents](https://nexus.lab.fiware.org/repository/raw/public/badges/chapters/iot-agents.svg)](https://github.com/FIWARE/catalogue/blob/master/iot-agents/README.md)
[![License: MIT](https://img.shields.io/github/license/fiware/tutorials.Iot-Agent.svg)](https://opensource.org/licenses/MIT)
[![Support badge](https://img.shields.io/badge/tag-fiware-orange.svg?logo=stackoverflow)](https://stackoverflow.com/questions/tagged/fiware)
[![JSON LD](https://img.shields.io/badge/JSON--LD-1.1-f06f38.svg)](https://w3c.github.io/json-ld-syntax/)

## General Setup

For the general setup of the digital twin of the SmartWorld by FIWARE (lego-demonstrator) have a look at the ```DigitalTwinFlowchart.pdf```. The Base of the hole digital twin is the lego-demonstrator itself with all its microcontrollers, actuators and sensors. The information of the sensors is transferred from the microcontrollers via WiFi to the ```mosquitto MQTT-Broker```. From there the ```IoT-Agent``` is reading this information, translating it into ```NGSI-LD``` and sending it to the ```Orion-LD context broker```. The current data of the lego-demonstrator is available in real time and standartized in the context broker. The Digital Twin representation in the website is getting its information from the context broker. When you want to see the data over time you need to store it somewhere else. For this task the context broker sends the new data to ```Quantumleap```, which stores the data in a ```Timescale-DB``` database. The dashboard-tool ```Grafana``` gets the information over time out of the database and show it in dashboards.

## Start up the context broker

1. Install docker and docker-compose
2. Start the context broker setup with stable internet connection:
```
./services orion
```
3. Stop the context broker:
```
./services stop
```

## Start up the context broker on fair without internet

Start the context broker setup without stable internet connection (recommended on fair):
```
./services orion+mongoRestore
```

When you do it the first time you have to once execute the following steps:
1. Start the context broker **with** an active internet connection:
```
./services orion
```
2. When everything is up and running do a dump of the mongo database:
```
./services mongoDump
```
3. Now you can start the context broker without an active internet connection:
```
./services orion+mongoRestore
```


## Import dashboards in Grafana




Have a look at ```mongoRestore/mongoRestore.md``` for more information.

---

## License

[MIT](LICENSE) © 2020 FIWARE Foundation e.V.
