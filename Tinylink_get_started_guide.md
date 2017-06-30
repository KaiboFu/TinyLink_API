TinyLink Get Started Guide
================

[TOC]

Welcome to the TinyLink get started guide. This guide takes you through the essential steps from setting up your development environment to running examples with the TinyLink system. The get started guide is divided into sections, each section includes summary steps.

# 1. What is TinyLink?
TinyLink is a holistic system for rapid development of IoT applications.

# 2.Preparations for using TinyLink
There are two steps for you to do the preparations for using TinyLink. After that, we will go through  examples.

## 2.1 Get the TinyLink hardware components
Theoretically, there is *NO NEED* for users to prepare the hardware components before using TinyLink.
However, in this getting started guide, we will go through prepared examples in the following section.
We need to prepare hardware components in the following table firstly.

|LinkIt ONE|Arduino UNO R3|SD Card Shield V4|Base Shield V2|Grove Light Sensor|Grove Temperature and Humidity Sensor|SDS018|Grove UART WiFi|
|-|-|-|-|-|-|-|-|
|**Soil Moisture Analog Sensor**|**Dupont Lines**|**Grove Port Cable**|**SD Card 2G**|**TF Card 2G**|**USB Cable Type B**|**Micro USB Cable**||

## 2.2 Get the TinyLink client for Windows
The TinyLink Client for Windows provides a comprehensive development environment for developing IoT applications via TinyLink.
With this client, you can upload the source file, retrieve the generated hardware configuration and the binary program, as well as burn the binary to the assembled device.

### 2.1.1 For Windows users

#### Download the client
* Download URL: [ftp://ftp.emnets.org/public/TinyLink/Tinylink_Client.zip](ftp://ftp.emnets.org/public/TinyLink/Tinylink_Client.zip)
* Unzip the TinyLink_Client.zip you have just downloaded.

#### Install the drivers

##### For LinkIt One development board
* Find the driver *InstallMTKUSBCOMPortDriver.exe* in the folder "*TinyLink_Client/drivers/*".
* Open it and follow the installation instructions.

##### For Arduino UNO development board
* Open **Control Panel** and search for and open **Device Manager**.
* Find the **Arduino Uno** in **Other devices**, due to the drivers for this device are not installed. 
* Double click the **Arduino Uno** and click **Update Driver...**. 
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/UpdateDriverUno_0.png)
* Follow the instructions below and update the driver.
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/UpdateDriverUno_1.png)
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/UpdateDriverUno_2.png)
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/UpdateDriverUno_3.png)
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/UpdateDriverUno_4.png)

### 2.1.2 For Linux users
We have been working on TinyLink Linux version, but it is not ready yet.

## 2.3 Register on TinyLink website
One should register on TinyLink website before he/she can develop an IoT application.

* Open the **TinyLink.exe** in **TinyLink_Client** folder.
* Click **"注册(Register)"** button on the right.
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Register_0.png)
* Fill in the blanks with the user's basic information, as well as the experience in IoT development.
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Register_1.png)
* After registration, we can click the **"登陆(Login)"** button on the right, and input the account information we have just registered.
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Register_2.png)

**Note: After all these steps above, we have completed the preparation for TinyLink.**

# 3. Learn Through TinyLink Examples
Now we can write our own source code to create IoT applications. We will present three examples here for better understanding.

## 3.1 LED blink
We will turn one of the boards LEDs on for one second and then off for one second, repeatedly.
This is an easy and common example.
### Step 1 - Write the source code
Here is the source code. Just copy it and save it to the local disk as "Blink.cpp".

	REQUIRE("Arduino UNO");
	
	void setup() {
	}
	
	void loop() {
	  TL_LED.toggle();
	  TL_Time.delayMillis(1000);
	}

### Step 2 - Upload the source code via TinyLink client
* Open the **TinyLink.exe**, and log in just in case.
* Select and upload the source code file **"Blink.cpp"** by clicking the submit button.
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Blink_0.png)
* After observing the success information, TinyLink generates the hardware configuration for the source code and cross-compiles the software system for the hardware. We can watch the hardware connection figure by clicking the **"硬件配置(Hardware Configuration)"** button. 
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Blink_1.png)
* Next, we will assemble the hardware for the application with the help of **connect.jpg** in the **configuration** folder. Since there is only one hardware component, Arduino UNO, in this example, we have completed the assembling procedure.
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Blink_2.png)
* Then, we will attach the assembled hardware to our computer. We plug the Type B USB cable into Arduino UNO on one side, and on the other side into the USB port on the computer.
* Afterwards, we will burn the software system onto the assembled hardware, i.e., Arduino UNO in this case. We just need to click the **"一键烧写(Click-and-burn)"** button, and wait until it is done.
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Blink_3.png)
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Blink_4.png)
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Blink_5.png)
* Finally, we have built our first IoT application, LED Blink, using TinyLink. Now we can observe that the LED on Arduino UNO is toggling every second.
## 3.2 Fetch Internet information via WiFi

## 3.3 A simple smart houseplant device
