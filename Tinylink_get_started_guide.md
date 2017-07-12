[TOC]

Welcome to the TinyLink get started guide. This guide takes you through the essential steps from setting up your development environment to running examples with the TinyLink system. The get started guide is divided into sections, each section includes summary steps.

# 1. What is TinyLink?
TinyLink is a **holistic** system for **rapid development** of IoT applications.  
Developers write the application code in C-like language to specify the key logic of their applications, without dealing with the details of hardware components.  
Taking the application code as input, TinyLink **automatically** generates hardware configurations as well as the hardware dependent code executable on the targeted hardware platform.

# 2.Preparations for using TinyLink
There are two steps for you to do the preparations for using TinyLink. After that, we will go through three examples.

## 2.1 Get the TinyLink hardware components
Theoretically, there is *NO NEED* for users to prepare the hardware components before using TinyLink.
However, in this getting started guide, we will go through prepared examples in the following section.
We need to prepare hardware components in the following table firstly.

<!--|LinkIt ONE|Arduino UNO R3|SD Card Shield V4|Base Shield V2|Grove Light Sensor|Grove Temperature and Humidity Sensor|SDS018|Grove UART WiFi|
|-|-|-|-|-|-|-|-|
|**Soil Moisture Analog Sensor**|**Dupont Lines**|**Grove Port Cable**|**SD Card 2G**|**TF Card 2G**|**USB Cable Type B**|**Micro USB Cable**||-->



|Component|Image|
|---|---|
|LinkIt_ONE|![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Devices/LinkIt_ONE.png)|
|Arduino_UNO_R3|![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Devices/Arduino_UNO_R3.png)|
|SD_Card_Shield_V4|![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Devices/SD_Card_Shield_V4.png)|
|Base_Shield_V2|![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Devices/Base_Shield_V2.png)|
|Grove_Light_Sensor|![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Devices/Grove_Light_Sensor.png)|
|Grove_Temperature_and_Humidity_Sensor|![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Devices/Grove_Temperature_and_Humidity_Sensor.png)|
|SDS018|![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Devices/SDS018.png)|
|Grove_UART_WiFi|![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Devices/Grove_UART_WiFi.png)|
|Soil_Moisture_Analog_Sensor|![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Devices/Soil_Moisture_Analog_Sensor.png)|
|Dupont_Lines|![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Devices/Dupont_Lines.png)|
|Grove_Port_Cable|![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Devices/Grove_Port_Cable.png)|
|SD_Card_2G|![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Devices/SD_Card_2G.png)|
|TF_Card_2G|![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Devices/TF_Card_2G.png)|
|USB_Cable_Type_B|![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Devices/USB_Cable_Type_B.png)|
|Micro_USB_Cable|![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Devices/Micro_USB_Cable.png)|

## 2.2 Get the TinyLink client for Windows
The TinyLink Client for Windows provides a comprehensive development environment for developing IoT applications via TinyLink.
With this client, you can upload the source file, retrieve the generated hardware configuration and the binary program, as well as burn the binary to the assembled device.

### 2.1.1 For Windows users

#### Download the client
* Download URL: [ftp://ftp.emnets.org/public/TinyLink/Tinylink_Client.zip](ftp://ftp.emnets.org/public/TinyLink/Tinylink_Client.zip)
* Unzip the TinyLink_Client.zip you have just downloaded.

#### Install the drivers

##### For LinkIt One development board
* Find the driver **InstallMTKUSBCOMPortDriver.exe** in the folder **drivers**.  
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/LinkIt_One_Driver.png)  
* Open it and follow the installation instructions.

##### For Arduino UNO development board
* Attach the Arduino UNO to a computer via  USB Cable Type B.
* Open **"Control Panel(控制面板)"** and open **"Device Manager(设备管理器)"**.
* Find the **Arduino Uno** in **Other devices**, due to the drivers for this device are not installed.  
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/UpdateDriverUno_0.png)   
* Double click the **Arduino Uno** and click **Update Driver...**.   
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
* We have implemented an online [API document](http://10.214.149.119/tinylink/view/api_page.php), where developers can search for their desired APIs. For example, we need to use **LED** module, we can search for "LED" and find the **TL_LED** library.
* Every TinyLink program contains two basic functions, the **setup()** function and the **loop()** function. The setup function deals with functions like module initialization, while the loop function are executed periodically after the setup function.
* Here is the source code. Just copy it and save it to the local disk as "Blink.cpp".

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

### Step 3 - Generate the hardware and the software
* Once the generation procedure is successful, there will be a status bar informing us.  
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Blink_1.png)
* Also, there will be some **Tips** about the generated hardware configuration. We should pay attention to them.
* After observing the success information, TinyLink generates the hardware configuration for the source code and cross-compiles the software system for the hardware. We can watch the hardware connection figure by clicking the **"硬件配置(Hardware Configuration)"** button.    

### Step 4 - Assemble the hardware components
Next, we will assemble the hardware for the application with the help of connection figure shown in **Hardware Connection**.

* We need to carefully look at the hardware components in the figure. The mainboard are not the same all the time. In this case, the mainboard is **Arduino UNO**.
* Since there is only one hardware component, Arduino UNO, in this example, we have completed the assembling procedure.   
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Blink_2.png)

### Step 5 - Burn the software system
* Then, we will attach the assembled hardware to our computer. We plug the Type B USB cable into Arduino UNO on one side, and on the other side into the USB port on the computer.
* Afterwards, we will burn the software system onto the assembled hardware, i.e., Arduino UNO in this case. We just need to click the **"一键烧写(Click-and-burn)"** button, and wait until it is done.  
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Blink_3.png)  
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Blink_4.png)  
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Blink_5.png)
* **Note that when the following text is shown, it means the program is burnt into Arduino UNO successfully.**  
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Blink_6.png)

### Step 6 - Watch the results
* Finally, we have built our first IoT application, LED Blink, using TinyLink. Now we can observe that the LED on Arduino UNO is toggling every second.

## 3.2 Upload the ambient light data to Internet via WiFi
Firstly, we will sample the ambient light in the form of integer numbers. Then we will upload the data to the cloud via WiFi every second. And finally we can observe the visualized data from both the website and the Android App.

The steps for creating this example is similar to the previous example.

### Step 1 - Register a node
* Click the tab **View Nodes** in **TinyLink_Client.exe**, and then click **Register a new node**.  
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Register_Node_0.png)  
* Input the **Node ID** and its **Description**, and register for this node.  
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Register_Node_1.png)
* Finish the registration.  
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Register_Node_2.png)

### Step 2 - Write the source code
* First, we need to generate the uploading URL for the code. Click the boxes after the intended items and then click the button **Generate URL**. Then the URL is generated as below. We need to replace the **xxx** in the URL with the sampled data before we use them.  
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Light_WiFi_URL.png)

* Here is the source code.  
Just copy it and save it to the local disk as "Light_WiFi.cpp".

		void setup() {
		  TL_WiFi.init();
		  TL_WiFi.join("EmNets-301", "eagle402");
		}
		
		void loop() {
		  TL_Light.read();
		  double l = TL_Light.data();
		  TL_WiFi.get("http://10.214.149.119/tinylink/receiveData.php?userid=12345&nodeid=100001&light=" + String(l));
		  TL_Time.delayMillis(1000);
		}

### Step 3~5 - Get the hardware and the software
Since they are similar to Steps 2-4 in the previous example, we will not discuss them in details.

* The included hardware components are listed as below.  

    |Component|Figure|
    |:---:|:---:|
    |Arduino UNO|![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Devices/Arduino_UNO_R3.png)|
    |Base Shield V2 (3.3V)|![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Devices/Base_Shield_V2.png)|
    |Grove UART WiFi|![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Devices/Grove_UART_WiFi.png)|
    |Grove Light Sensor|![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Devices/Grove_Light_Sensor.png)|

* The hardware connection figure is shown as below.  
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Light_WiFi_Figure.png)
* The assembled node is shown as below.  
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Light_WiFi_Real.png)

### Step 6 - Burn the software system
**Note that when connect any hardware component to UART port (or D0, D1 pins) on Arduino UNO, we shall NOT connect the component BEFORE we upload the software system.**  
We first upload the binary program, and then connect the hardware component.  
We set an interval of 10 seconds in the code, which is long enough for us finish connecting the WiFi module. 

### Step 7 - Watch the visualized results
* Watch the visualized data in tab **Display Data** of **TinyLink_Client.exe** by choosing the right Node ID (i.e., 100001) from the **Nodes List**.  
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Light_WiFi_Display.png)  
* **Note that if there is no data displayed in this page, there may be something wrong with the uploading procedure. A simple method to solve this is to press the RESET button on the Arduino UNO.**  
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Light_WiFi_Reset.png)   
* Download the Android App [**TinyLink.apk**](ftp://ftp.emnets.org/public/TinyLink/TinyLink.apk) and install it.
* Open the Android App, log in with our account and observe the uploaded data.  
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Android_App_0.png)

## 3.3 A simple smart houseplant device
After the two basic examples above, we will try a challenging example which is to build a smart node for houseplant.  
This node aims at monitor the ambient light and soil humidity of the houseplant every two seconds, and upload the data the cloud as well as save them in the local storage in case of network failure.

### Step 1 - Write the source code

	TL_File fp;
	
	void setup() {
	  TL_Serial.begin(9600);
	  TL_WiFi.init();
	  TL_WiFi.join("EmNets-301", "eagle402");
	  TL_Storage.begin();
	  fp = TL_Storage.open("test.txt", "w");
	}
	
	void loop() {
	  if (TL_Serial.available()) {
        fp.close();
        while (true);
	  }
	  TL_Light.read();
	  TL_Soil_Humidity.read();
	  double l = TL_Light.data();
	  double s = TL_Soil_Humidity.data();
	  TL_Serial.println(String("Light: ") + l + " Soil:" + s);
	  
	  String url = String("http://10.214.149.119/tinylink/receiveData.php?userid=12345&nodeid=100001&");
	  url = url + "light=" + l + "&soil_humidity=" + s;
	  TL_Serial.println(url);
	  bool res = TL_WiFi.get(url);
	  if (res == true) {
	    TL_Serial.println(String("Successfully send data via WiFi"));
	  } else {
	    TL_Serial.println(String("Fail to send data via WiFi"));
	  }
	  
	  int cc = fp.write(String(l) + String(", ") + String(s));
	  TL_Serial.println(String("Write ") + String(cc) + String(" char into storage"));
	  
	  TL_Time.delayMillis(2000);
	}

In this example, we use five different modules, which are **Serial, WiFi, Storage, Light, Soil_Humidity**.

### Step 2~5 - Get the hardware and the software, and burn the software into the assembled node
* Since they are similar to the previous example, we will not discuss them in details. The main difference is that the mainboard, LinkIt One, is used in the final hardware platform. LinkIt One contains the built-in storage module and the built-in WiFi module. **Note that the WiFi antenna should be attached to the reverse side of LinkIt One.**

* The included hardware components are listed as below.

    |Component|Figure|
    |:--:|:--:|
    |LinkIt One|![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Devices/LinkIt_ONE.png)|
    |Base Shield V2 (5V)|![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Devices/Base_Shield_V2.png)|
    |Grove Light Sensor|![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Devices/Grove_Light_Sensor.png)|
    |Soil Moisture Analog Sensor|![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Devices/Soil_Moisture_Analog_Sensor.png)|

* The hardware connection figure is shown as below.  
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/LinkIt_One_Connection.png)  
* **Note that the Soild Humidity Analog Sensor utilizes dupont lines to attach to A2 pin on the LinkIt One. We should be careful when attaching the dupont lines. It may cause permenant damage to the sensor if we connect the positive pin and negative pin in a contrary way.** The clear figure of the connection between the LinkIt One and the Soil Humidity Analog Sensor is shown as below.
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/LinkIt_One_Soil.png)
* We can visit the pinout diagram for both mainboards on the website for more details.  
    [Arduino Uno Pinout Diagram](http://10.214.149.119/tinylink/view/document/Arduino_Uno_Pinout.jpg)  
    ![Arduino Uno Pinout Diagram](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/Arduino_Uno_Pinout.jpg)  
    [LinkIt One Pinout Diagram](http://10.214.149.119/tinylink/view/document/LinkIt_One_Pinout.pdf)
    ![Arduino Uno Pinout Diagram](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/LinkIt_One_Pinout.png)  
* The assembled hardware platform is shown as below.   
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/LinkIt_One_Real.png)

### Step 6 - Watch the visualized results
This time, we can observe data from two difference sensors, including the Grove Light Sensor and the  Soil Humidity Sensor.
 
* The visualization page on the website is shown as below.  
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/LinkIt_One_Display.png)  
* Also, we can observe the results through Serial port. We can click on the **"Open Serial(打开串口)"** to start the **"OpenJumper串口调试器.exe"**.  
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/LinkIt_One_Serial_0.png) 
* Then we click on **"Open Serial(打开串口)"** and watch the results printed in the received area. We should close the Serial by clicking on **"Close Serial(关闭串口)"** once we have done observing.  
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/LinkIt_One_Serial_1.png)  
    ![](ftp://ftp.emnets.org/public/TinyLink/GuideFigure/LinkIt_One_Serial_2.png) 

# 4. Start Your Journey
Now it is time you should start your journey with TinyLink.  
Do not forget to finish the experiment report after you have done all the experiments.  
Good luck!