# Introduction

The goal of the **cloud.iO modbus gateway** is to connect modbus devices to **cloud.iO** in a modular way, only by writing **configuration files**.

The cloudio modbus gateway source code can be found [here](https://github.com/cloudio-project/cloudio-modbus-gateway/). <br>
This repository is mainly composed of the *src* directory, which contains the source code and the *settings* directory, which contains an example of filled config files.

## Files types

- **Device model**: describes the device modbus registers structure.
- **Data model**: describes the cloudio structure for a device.
- **Mapping**: describes the mapping between a [device model](http://localhost:35908/#/modbus-cloudio-gateway/device_model) and a [data model](http://localhost:35908/#/modbus-cloudio-gateway/data_model).
- **Cloud.iO properties**: describes the cloud.iO connection information.
- **Gateway configuration**: links all the other files together.

## How to run

1. Clone the [cloudio-modbus-gateway](https://github.com/cloudio-project/cloudio-modbus-gateway/) repository.
2. Install the required libraries :
		pip install -r requirements.txt
3. Add or create your settings files into the settings directory.
4. Set the `GATEWAY_CONFIG` environment variable to the gateway configuration file name you want to use.
5. Run `src/main.py`:
		python src/main.py