# Wio Terminal Azure IoT sample

This repo shows sample code for connecting the Wio Terminal to Azure IoT Hub. This uses the [Azure Arduino SDK](https://github.com/Azure/azure-iot-pal-arduino).

This code connects to IoT Hub, then sends telemetry in the `loop` function. It also listens to direct method requests.

The IoT Hub code runs single-threaded, so you need to call `IoTHubDeviceClient_LL_DoWork(_device_ll_handle)` to process messages from IoT Hub. Instead of a long `delay` in the `loop` function, this code shows how to implement a long delay as lots of short delays with calls to `IoTHubDeviceClient_LL_DoWork`.

When your device connects, part of the internal connection logic uses the current time to build a key. This means the device time has to be correct, and this is implemented in the `ntp.h` file, with code to get the current time from an NTP server and set it on the Wio Terminals RTC.

## Instructions

1. Create an Azure IoT Hub
1. Create a device and get the connection string
1. Open this folder in VS Code using the PlatformIO extension
1. Set the `CONNECTION_STRING` constant in `config.h` in the `src` folder to the device connection string
1. Set the `SSID` and `PASSWORD` constants in `config.h` in the `src` folder to the relevant values for your WiFi
1. Build and deploy to your Wio Terminal using PlatformIO

> If you are using the Arduino IDE, you can copy the `main.cpp` code into your sketch file, and add the other files in the `src` folder into your sketch folder. You will need to choose the Wio Terminal in the board manager and add the following libraries using the library manager:
>
> * bblanchon/ArduinoJson
> * seeed-studio/Seeed Arduino rpcWiFi
> * seeed-studio/Seeed Arduino FS
> * seeed-studio/Seeed Arduino SFUD
> * seeed-studio/Seeed Arduino rpcUnified
> * seeed-studio/Seeed_Arduino_mbedtls
> * seeed-studio/Seeed Arduino RTC
> * arduino-libraries/AzureIoTHub
> * azure/AzureIoTUtility
> * azure/AzureIoTProtocol_MQTT
> * azure/AzureIoTProtocol_HTTP
> * azure/AzureIoTSocket_WiFi
