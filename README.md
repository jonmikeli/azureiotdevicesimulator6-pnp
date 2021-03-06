# Azure IoT Device Simulator 6 PnP - IoT Plug and Play version - Readme

This project has for purpose to help IoT developers and testers. The solution is an Azure IoT Device simulator coded with .NET 6 (C#) that implements different types of Cloud To Device (C2D) / Device To Cloud (D2C) flows between [Microsoft Azure IoT Hub](https://azure.microsoft.com/en-us/services/iot-hub/) and the simulated device.

This version of the simulator is based on the [regular version of the simulator](https://github.com/jonmikeli/azureiotdevicesimulator6), which in turn, completes the series of simulators created on top of:
 - [.Net Core 2.1](https://github.com/jonmikeli/azureiotdevicesimulator)
 - [.Net Core 3.1](https://github.com/jonmikeli/azureiotdevicesimulator3)
 - [.Net Core 5.0](https://github.com/jonmikeli/azureiotdevicesimulator5)


IoT Plug and Play is meant to facilitate the integration of IoT devices with IoT solutions. It tries to imitate the concept of the already known Plug and Play experience at computers level.

The implementation follows a no-typed approach when it comes to DTDL parsing. The initial purpose was to protect the solution against possible changes in the DTDL definition. A not typed approach is less prone to structural updates when the model evolves frequently. However, DTDL v2 seems quite stable now (I could even expect a DTDL v3 quite soon). So, I guess a new implementation following a typed approach would be more appropriate now.

Besides the aforementioned simulators, a version implementing [Device Provisioning Service (DPS) features](https://github.com/jonmikeli/azureiotdevicesimulator6-dps) completes the family of simulators. This separation between PnP and other simulators is kept since DTDL does not cover some types of needs.
So, both approaches are kept.
It could be useful thought to add DPS features to the PnP IoT Simulator.

## DTDL (Digital Twin Definition Language)

This simulator allows to use [DTDL, Digital Twin Definition Language](https://github.com/Azure/opendigitaltwins-dtdl/blob/master/DTDL/v2/dtdlv2.md) models. These models describe the device capabilities via the next concepts:
 - components
 - interfaces
 - properties
 - telemetries
 - commands
 - relationships

All these are described in detail [here](https://github.com/Azure/opendigitaltwins-dtdl/blob/master/DTDL/v2/dtdlv2.md).

DTDL is based on open standards (JSON-LD and RDF).

The concepts integrated in this simulator are:
 - components
 - interfaces
 - properties (the parser extracts writable and readble properties. The desired properties are checked with the writable properties to verify if they are coherent.)
 - telemetries
 - commands


![Simulator process](docs/images/DTDLv2.png)


## Models

DTDL v2 does not allow using more than a schema per model.
However, some devices may need sending different types of messages.
To overcome this limitation, the similator may be used with a list of DTDL models.
Only one model is loaded at a time (default model) to keep coherence and integrity.


## Additional details

 - [*How to (Quickstart)*](docs/HowTo.md)
 - [*Help and details*](docs/Help.md) 
 
## Examples of use

 - development tool for developers working on Microsoft Azure IoT solutions (cloud)
 - tester tool in IoT-oriented projects
 - scalable IoT simulation platforms
 - fast and simple development of IoT devices
 - etc

## Technical information

 - .NET 6 (C#)
 - Microsoft Azure IoT SDK (Device capabilities, including IoT Hub modules, a.k.a. module identities)
 - IoT Plug and Play
 - DTDL v2

<br/>

> IOT PLUG AND PLAY VS REGULAR SIMULATOR
>
> You can find [here](https://github.com/jonmikeli/azureiotdevicesimulator6) a conventional version of the simulator (without IoT Plug and Play).
> The main difference with the IoT Plug and Play version is that it allows to easily handle with complex JSON Schemas and different types of mesages in one single device.
>
> _Which one to choose?_
> The regular simulator is recommended in contexts where:
>  - the device needs to send different types of messages.
>  - the messages will follow complex formats.
>  - you do not want implement DTDL models or use IoT Plug and Play features.
>  - DTDL v2 does not allow to implement what you need (ex: different schemas for one single message).
>
> The IoT PnP simulator is recommended in contexts where:
> - the DTDL models need to be tested.
> - the IoT Plug and Play flows need to be tested.
> - you already have one or many DTDL models and want to simulate the device fast and easily.
> - you need to integrate your device with IoT solutions (cloud) with IoT Plug and Play capabilities.

<br/>

*Azure IoT Device Simulator logs*

![Azure IoT Device Simulator Logs](docs/images/AzureIoTDeviceSimulatorLos.gif)

<br/>

## Global features

 - device level simulation (C2D/D2C)
 - module level simulation (C2M/M2C)
 - device simulation configuration based on JSON files
 - module simulation configuration based on JSON files
 - no specific limitation on the number of modules (only limited by Microsoft Azure IoT Hub constraints)
 - simple and lightweight application, containerizable
 - implementation of full IoT flows (C2D, D2C, C2M, M2C) - see below for more details


## Functional features

### Device level (C2D/D2C)

*Commands*
 - request latency test
 - reboot device
 - device On/Off
 - read device Twin
 - generic command (with JSON payload)
 - generic command
 - update telemetry interval
 
 *Messages*
 D2C: The device will send the telemetries according the referenced DTDL model.
 
 C2D: Microsoft Azure IoT Hub can send messages to a given device.
 
 *Twin*
 Any change in the Desired properties is notified and handled by the device.


### Module level (C2M/M2C)

Commands have also been implemented at device module level.

>NOTE
>
>Latency tests will not be included at modules level.

  
## Global technical features

Functional features are based on these generic technical features:
 - telemetry sent from a device.
 - a device may contain one or many modules.
 - each module behaves independently with its own flows (C2M/M2C) and its configuration settings.
 - the device that contains the modules has its own behavior (based on its own configuration file).
 - telemetry sent from a module.
 - messages received by a device.
 - messages received by a module.
 - commands received by a device.
 - commands received by a module.
 - Twin Desired properties changed notification (for devices).
 - Twin Desired properties changed notification (for modules).
 - Twin Reported properties updates from a device.
 - Twin Reported properties updates from a module.


## More information

- Details about **HOW the solution WORKS** are provided in the [help](docs/Help.md) section.
- Details about **HOW the solution can be USED** are provided in the [how to](docs/HowTo.md) section.
