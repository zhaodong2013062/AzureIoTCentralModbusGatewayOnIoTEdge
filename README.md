# IoT Edge module for a Iot Central gateway for Modbus devices

This is an IoT Edge module that runs on Linux or Windows devices to function as a Modbus Gateway to IoT Central. The module runs on an IoT Edge device in an IoT Hub, but sends telemetry and receives settings from an IoT Central device. Usage of your device is done entirely through the IoT Central app - the IoT Hub exists only to create the IoT Edge runtime.

## Prerequisites 

### IoT Edge
Before using this module, you should be familiar with setting up an Edge device and deploying Edge modules. If you are not yet familiar with these concepts, the following guides are strongly recommended:
- [Deploy your first IoT Edge module to a Linux device](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart-linux)
- [Develop and deploy a Python IoT Edge module for Linux devices](https://docs.microsoft.com/en-us/azure/iot-edge/tutorial-python-module)
- [Use Visual Studio Code to develop and debug modules for Azure IoT Edge](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-vs-code-develop-module)

For windows versions of these guides:


### Software
- [Docker](https://www.docker.com/products/docker-desktop) installed and running on your dev box.
- [Python 2.7.X](https://www.python.org/downloads/)

## Run the module on an Edge device against a simulated Modbus device
1. Create and set up an IoT Central app by following the **Creating Azure Resources** section of the [IoT Central Gateway for Modbus Devices Readme](https://github.com/zhaodong2013062/Azure_IoT_Central_Modbus_Gateway). 

2. Populate the **IoT Central parameters** section of `modules/ModbusGatewayPythonModule/config.py`. Since we are running against a simulated Modbus device, there is no need to configure the **Modbus parameters** section.

3. Create an IoT Hub and register an IoT Edge device to the IoT Hub. If you are not sure how to do this, follow [Deploy Your First IoT Edge Module](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart-linux) until **Deploy a module**. We will be deploying this module instead of an Azure Marketplace module. 

4. Follow the **Build and push your module** and **Deploy modules to device** sections of [Develop and deploy a Python IoT Edge module for Linux devices](https://docs.microsoft.com/en-us/azure/iot-edge/tutorial-python-module).

5. In your IoT Central app, you should be able to see a new device created under the **Gateway** template named `modbusmastertests`. Paste the contents of `modules/ModbusGatewayPythonModule/sampleconfig.txt` into the `SlavesConfig` setting for the new device. After the Edge device finishes setup, you should see a new **MXChip** slave device with simulated Modbus data.

## Running the module against real Modbus devices
1. Set up a real IoT Edge device and register it to IoT hub. 

2. Physically connect the IoT Edge device to the desired Modbus devices.

3. Configure the **IoT Central parameters and **Modbus parameters** sections of `modules/ModbusGatewayPythonModule/config.py`. 

3. Create and push a config file to the master device. Details of the config file structure can be found [here](https://github.com/zhaodong2013062/Azure_IoT_Central_Modbus_Gateway#config-file-structure-and-explanation).

4. Deploy the module to your real device, and you should see the data from your Modbus device your IoT Central app!