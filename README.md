![header](doc/header.png)

# IoT Multiprotocol Dashboard

Author: Agustin Bassi - 2020

## 
## Table of Contents


* [Platform Introduction](#platform-introduction)
* [Install dependencies](#install-dependencies)
* [Run the application](#run-the-application)
* [Test the application](#test-the-application)
* [Run mqtt-client-arduino (optional)](#run-mqtt-client-arduino-(optional))
* [Want to help?](#want-to-help-?)
* [License](#license)

## 
## Platform Description

The goal of this project is to create an IoT multiprotocol dashboard based in Node-RED and running it with Docker Compose.

The platform consists in several modules described below.

* **Node-RED**: Node-RED is a platform to easily develop IoT application based in a powerful visual programming blocks. It was developed by IBM and now maintainer by a huge community.
* **MQTT Broker**: Raspberry Pi that runs a MQTT Broker to interact with the HTTP client via WebSockets and to MQTT clients via MQTT protocol. Besides, has a HTTP server in order to serve the page of the HTTP Client.
* **MQTT Device** (optional): An embedded firmware running in Arduino based boards which supports MQTT like ESP32 or ESP8266. This piece of the project is optional and whole features can be tested via terminal.

In the figure below there is a description of the application modules and how they interact each others.

![architecture](doc/architecture.png)

## 
## Install dependencies


The application runs over Raspberry Pi 3+. To install Raspberry Pi OS refer to [official documentation](https://www.raspberrypi.org/documentation/installation/installing-images/).

The platform needs the next dependencies.

* Docker & Docker-Compose (installation steps in [this link](https://devdojo.com/bobbyiliev/how-to-install-docker-and-docker-compose-on-raspberry-pi)).

_Although the application is designed to run on a Raspberry Pi 3+, it can runs on any system with Docker & Docker Compose installed. Docker installation steps in [official documentation](https://docs.docker.com/get-docker/). Docker-Compose installation steps in [official documentation](https://docs.docker.com/compose/install/)._

## 
## Run the application

Once dependencies are installed in the Raspberry Pi do the next steps.

1. Download the platform code (this repository) with the next command.

```
git clone https://github.com/agustinBassi/nodes-connection.git
cd nodes-connection/
```

2. Start the application with the next command.

```
docker-compose up
```

3. Go to application's dashboard opening [http://host_ip:1880/ui](http://host_ip:1880/ui) in the web browser. You should see a dashboard like below.

![architecture](doc/architecture.png)


## 
## Test the application

The dashboard gets two-ways communication: from devices to dashboard & from dashboard to devices.

### From Devices to dashboard

Once the Node-RED dashboard is running (previous step), publish a message using the mosquitto_pub client which are bundled into the Mosquitto Docker container with the next command:

```sh
docker exec -it mosquitto mosquitto_pub -t "device/status/esp32-001" -m "{'temperature': 19, 'humidity': 77}"
```

After the MQTT topic is published, the values must be shown in the dashboard. Publish other values to see them in the chart widgets. 

### From Dashboard to devices

To test the communication from dashboard to devices, subscribe to any topic using mosquitto_sub client bundled into Mosquitto Docker container with the next command.

```sh
docker exec -it mosquitto mosquitto_sub -t "#"
```

Then, in the `MQTT Messages` section in the dashboard, set a topic to send, a message and press `Publish`. The content of the message should be shown into the terminal where the mosquitto_sub command was executed.


## 
## Useful commands



## 
## Want to help?

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change. If someone want to helpme, every bit of effort will be appreciated. 

If you find it useful please helpme following my Github user and give a Star to this project. This will animate me to continue contribuiting with the great open source community.

## 
## License

This project is licensed under the GPLV3 License.

![footer](doc/footer.png)