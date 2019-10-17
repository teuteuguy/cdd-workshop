# Building AWS Connected Drink Dispenser Workshop

This repository contains Amazon FreeRTOS code that listens to shadow shanges and controls motor and WS2812b addressible LED ring. In order to compile the code in the Cloud9 environment please execute following sections:

## Option 1: build in AWS Cloud9
Note: (Requires an AWS Accout) 

- [Setting up Cloud9 Environment](./Cloud9.md)
- [Installing ESP32 toolchain](./ToolchainSetup.md)
- [Compiling Amazon FreeRTOS code](./CompilingWorkshopFW.md)


## Option 2: build on your laptop

### Setup the tools on your computer

To communicate with your board, you need to download and install a toolchain.
To set up the toolchain, follow the instructions for your host machine's operating system:

*Note: When you reach the "Get ESP-IDF" instructions under Next Steps, stop and return to the instructions on this page. If you previously followed the "Get ESP-IDF" instructions and installed ESP-IDF, make sure that you clear the IDF_PATH environment variable from your system before continuing.
*

[Standard Setup of Toolchain for Windows](https://docs.espressif.com/projects/esp-idf/en/v3.1.5/get-started-cmake/windows-setup.html)

[Standard Setup of Toolchain for macOS](https://docs.espressif.com/projects/esp-idf/en/v3.1.5/get-started-cmake/macos-setup.html)

[Standard Setup of Toolchain for Linux](https://docs.espressif.com/projects/esp-idf/en/v3.1.5/get-started-cmake/linux-setup.html)

### Compile the code



1. Clone the repo:

```bash
cd ~/Downloads
git clone https://github.com/teuteuguy/cdd-workshop
```

2. Format your credentials

Navigate to [CredFormatter](https://yona75.github.io/credformatter/), upload Certificate and Private key provided to you and generate aws_clientcredential_keys.h file. 

Download the file to: ~/Downloads/cdd-workshop/demos/common/include

3. Copy aws_clientcredential.h template and rename it

```bash
cp ~/Downloads/cdd-workshop/tools/aws_config_quick_start/aws_clientcredential.templ ~/Downloads/cdd-workshop/demos/common/include/aws_clientcredential.h
```

4. Edit the aws_clientcredential.h file to change following values
 
- Please note that clientcredentialWIFI_SECURITY defined without double quotes
- Also, the thing name is the number associated with your drink dispenser

```bash
EXAMPLE: #define clientcredentialIOT_THING_NAME "203"
```

```bash
static const char clientcredentialMQTT_BROKER_ENDPOINT[] = <"Will be provided">;
#define clientcredentialIOT_THING_NAME  <"thing name provided to you individually">
#define clientcredentialWIFI_SSID       <"WillBeProvided">
#define clientcredentialWIFI_PASSWORD   <"WillBeProvided">
#define clientcredentialWIFI_SECURITY   eWiFiSecurityWPA2
```

7. Build

```bash
cd ~/Downloads/cdd-workshop/demos/espressif/esp32_devkitc_esp_wrover_kit/make
make menuconfig
```

8. Click *Save* and then *Exit*
9. Execute *make* command

```bash
make
```

### Flash the device

- [Uploading compiled firmware to ESP32 development board](./FlashingFW.md)