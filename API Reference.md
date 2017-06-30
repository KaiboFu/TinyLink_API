[TOC]
# Core API

## String library
The String library is a new string library which will run well in all platforms for TinyLink. Since not all platforms support the C++ string library (e.g., the Arduino Serials), we just design our own String library. For convenience, we just take example by the classic string library for Arduino which is well designed and small enough for some memory constrained embedded platform. So this String library is just the same as that of Arduino (just refer to https://www.arduino.cc/en/Reference/StringObject ) and people who are familiar with Arduino will get started quickly with it. 

### String Module(String class)
The String class allows you to use and manipulate strings of text in more complex ways character arrays. You can concatenate Strings, append to them, search for and replace substrings and more. It takes more memory than a simple character array, but it is also more useful and powerful.
For reference, character arrays are referred to as small s, and instances of the String class are referred to as String with a capital S. Note that constant strings, specified in “double quotes” are treated as char arrays, not instances of the String class. For descriptions of functions and operators of the String class, please refer to [String for Tinylink](https://www.arduino.cc/en/Reference/StringObject).


## TL_Serial library
TL_Serial library is used for communication between the development boards and a computer or other devices. Serial communication on pins TX/RX uses TTL logic levels (5V or 3.3V depending on the board). All the development boards provided by TinyLink have at least one serial port (also know as a UART or USART). Through serial module, you can send/receive any information to/from annother board or device.

### Serial Module

#### begin()
+ **Description**
    Before using serial, the data rate in bits per second (baud) must be set for transmission. For communicating with the computer, use one of these rates: 300, 600, 1200, 2400, 4800, 9600, 14400, 19200, 28800, 38400, 57600, or 115200. You can, however, specify other rates. For communication between two devices, the data rate must be set at the same value.
+ **Syntax**
    void begin(unsigned long speed)
+ **Parameters**
    **speed**: in bits per second (baud)
+ **Return**
    none
+ **Usage**
    TL_Serial.begin(speed)
+ **Example**
```c++
void setup() {
    // Initialize the serial and set the data rate.
    TL_Serial.begin(9600);
    TL_Serial.println("Hello TinyLink");
}

void loop() {
}
```

#### end()
+ **Description**
    Disables serial communication, allowing the RX and TX pins to be used for general input and output. To re-enable serial communication, call TL_Serial.begin().
+ **Syntax**
    void end()
+ **Parameters**
    none
+ **Return**
    none
+ **Usage**
    TL_Serial.end()
+ **Example**
```c++
void setup() {
    // Initialize the serial and set the data rate
    TL_Serial.begin(9600);
    TL_Serial.println("Hello TinyLink");
    // Disables the serial
    TL_Serial.end();

}

void loop() {
}
```

#### available()
+ **Description**
    Gets the number of bytes (characters) available for reading from the serial port. This is data that's already arrived and stored in the serial receive buffer(which holds 64 bytes just for Arduino UNO). 
+ **Syntax**
    int available()
+ **Parameters**
    none
+ **Return**
    **int**: the number of bytes available to read; if there is nothing available the returning     number is 0; if there is something wrong with the serial the returning number is negative
+ **Usage**
    TL_Serial.available()
+ **Example**
```c++
void setup() {
    // Initializes the serial
    TL_Serial.begin(9600);
    // Block here until the serial receives a char
    while(!TL_Serial.available());
}

void loop() {
}
```

#### read()
+ **Description**
    Reads the first byte of incoming serial data.
+ **Syntax**
   int read()
+ **Parameters**
    none
+ **Return**
    **int**: the first byte of incoming serial data available (or -1 if no data is available)
+ **Usage**
    TL_Serial.read()
+ **Example**
```c++
int comingByte = 0;
void setup() {
    // Initializes the serial
    TL_Serial.begin(9600);
}

void loop() {
    // Check whther there is some data available for reading from the serial
    if(TL_Serial.available()) {
        // Read the coming data
        comingByte = TL_Serial.read();
        TL_Serial.print("I receive: ");
        TL_Serial.println(comingByte);
    }
}
```

#### print()
+ **Description**
    Prints data to the serial port as human-readable ASCII text. This command can take many forms. Numbers are printed using an ASCII character for each digit. Floats are similarly printed as ASCII digits, defaulting to two decimal places. Bytes are sent as a single character. Characters and strings are sent as is, e.g., TL_Serial.print(78) gives "78", TL_Serial.print(78.123) gives "78.12",  TL_Serial.print('a') gives "a" and TL_Serial.print('abc') gives "abc"
+ **Syntax**
    int print(char val)
    int print(int val)
    int print(long val)
    int print(double val)
    int print(const char* val)
    int print(const String &val)
+ **Parameters**
    **val**: the value to print
+ **Return**
    **int**: the number of bytes written, though reading that number is optional
+ **Usage**
    TL_Serial.print(val)
+ **Example**
```c++
int comingByte = 0;
void setup() {
    // Initializes the serial
    TL_Serial.begin(9600);
}

void loop() {
    // Send the data back if you receive some data
    if(TL_Serial.available()) {
        // Read the coming data
        comingByte = TL_Serial.read();
        // Send what you get
        TL_Serial.print("I receive: ");
        TL_Serial.println(comingByte);
    }
}
```

#### println()
+ **Description**
    Prints data to the serial port as human-readable ASCII text followed by a carriage return character (ASCII 13, or '\r') and a newline character (ASCII 10, or '\n'). This command takesthe same forms as TL_Serial.print().
+ **Syntax**
    int println(char val)
    int println(int val)
    int println(long val)
    int println(double val)
    int println(const char* val)
    int println(const String &val)
+ **Parameters**
    **val**: the value to print 
+ **Return**
    **int**: the number of bytes written, though reading that number is optional
+ **Usage**
    TL_Serial.println(val)
+ **Example**
```c++
int comingByte = 0;
void setup() {
    // Initializes the serial
    TL_Serial.begin(9600);
}

void loop() {
    // Send the data back if you receive some data
    if(TL_Serial.available()) {
        // Read the coming data
        comingByte = TL_Serial.read();
        // Send what you get
        TL_Serial.print("I receive: ");
        TL_Serial.println(comingByte);
    }
}
```



## TL_Time library
The TL_Time library provides some basic TIME functions, e.g. delaying the specific time, getting the current time, etc.

### Time Module

#### millisFromStart()
+ **Description**
    Returns the number of milliseconds since the board began running the current program. This number will go back to zero after overflow occurs.
+ **Syntax**
    unsigned long millsFromStart()
+ **Parameters**
    none
+ **Return**
    **unsigned long**: Number of milliseconds since the program started
+ **Usage**
    TL_Time.millisFromStart()  
+ **Example**
```c++
// Print the time since the board began in millisecond
void setup() {
    unsigned long time_Millis_Cur = TL_Time.millisFromStart();
    TL_Serial.print("The time since the board began in millisecond is ");
    TL_Serial.println(time_Millis_Cur);
}

void loop() {

}
```


#### microsFromStart()
+ **Description**
    Returns the number of microseconds since the board began running the current program. This number will go back to zero after overflow occurs.(There are 1,000 microseconds in a millisecond and 1,000,000 microseconds in a second)
+ **Syntax**
    unsigned long microsFromStart()
+ **Parameters**
    none
+ **Return**
    **unsigned long**: Number of microseconds since the program started
+ **Usage**
    TL_Time.microsFromStart()
+ **Example**
```c++
// Print the time since the board began in microsencod
void setup() {
    unsigned long time_Micros_Cur = TL_Time.microsFromStart();
    TL_Serial.print("The time since the board began in microsecond is ");
    TL_Serial.println(time_Micros_Cur);
}

void loop() {

}
```


#### delayMillis()
+ **Description**
    Pauses the program for the amount of time (in milliseconds) specified as parameter. (There are 1000 milliseconds in a second.)
+ **Syntax**
    void delayMillis(unsigned long ms)
+ **Parameters**
    none
+ **Return**
    **ms**: the number of milliseconds to pause
+ **Usage**
    TL_Time.delayMillis(ms)
+ **Example**
```c++
void setup() {
    TL_Serial.begin(9600);
}

void loop() {
    // Print "Hello TinyLink" in a interval of 1s
    TL_Serial.println("Hello TinyLink");
    TL_Time.delayMillis(1000);
}
```


#### delayMicros()
+ **Description**
    Pauses the program for the amount of time (in microseconds) specified as parameter. There are a thousand microseconds in a millisecond, and a million microseconds in a second.
+ **Syntax**
    void delayMicros(unsigned long us)
+ **Parameters**
    none
+ **Return**
    **us**: the number of microseconds to pause
+ **Usage**
    TL_Time.delayMicrosus)
+ **Example**
```c++
void setup() {
    TL_Serial.begin(9600);
}

void loop() {
    // Print "Hello TinyLink" in a interval of 1s
    TL_Serial.println("Hello TinyLink");
    TL_Time.delayMicros(1000000);
}
```


## TL_Timer library
The TL_Timer library provide the basic functions of the software timer interruption

### Timer Module
Timer Module provides an artificial data type Timer, which refers to a software timer. Users can start and stop a software timer and set the callback function, period of the software timer.

#### start()
+ **Description**
    Before using a timer, the timer must be started. A timer can only be started once(unless you have stopped it)
+ **Syntax**
   bool start()
+ **Parameters**
    none
+ **Return**
    **bool**: true on success; false on failure
+ **Usage**
  TL_Timer.start()
  ***or***
  TL_Timer1.start()
  ***or***
  TL_Timer2.start()
  ***or***
  ………
  ***or***
  TL_Timern.start()
  (Note: n is a numberic that is less than 8 and we provide 8 software timers for users)

#### stop()
+ **Description**
    Stops the timer(if you want to reuse the timer, you must start the timer again)
+ **Syntax**
   bool stop()
+ **Parameters**
    none
+ **Return**
    **bool**: true on success; false on failure
+ **Usage**
  TL_Timer.stop()
  ***or***
  TL_Timer1.stop()
  ***or***
  TL_Timer2.stop()
  ………
  ***or***
  TL_Timern.stop()
+ **Example**
```c++
void setup() {
    // Other codes
    ...
    // Start the timer
    TL_Timer.start();
    // Other codes
    ...
    //Stop the timer
    TL_Timer.stop();
}

void loop() {
}
```

#### attachInterrupt()
+ **Description**
    Attaches the callback function to a Timer object. When the timer expires, the callback function will be executed.
+ **Syntax**
    void attachInterrupt(void (* callback) ())
+ **Parameters**
    **callback**: the callback function for a Timer object,
+ **Return**
    none
+ **Usage**
    TL_Timer.attachInterrupt(callback)
    ***or***
    TL_Timer1.attachInterrupt(callback)
    ***or***
    TL_Timer2.attachInterrupt(callback)
    ………
    ***or***
    TL_Timern.attachInterrupt(callback)
    (Note: n is a numberic that is less than 8 and we provide 8 software timers for users. The users need to write the callback function by themselves )
+ **Example**
```c++
// Print the times the timer expires in a interval of 1s
int i = 0;
void callback() {
    TL_Serial.println("Timer expires " + String(i++) + "times");
}
void setup() {
    TL_Serial.begin(9600);
    // Set the period 
    TL_Timer.setPeriod(1000, TIMER_PERIODIC);
    // Attach the callback function to the timer. When the timer expires, the callback function will be excuted
    TL_Timer.attachInterrupt(callback);
    // Start the timer
    TL_Timer.start();
}

void loop() {
}
```


#### detachInterrupt()
+ **Description**
    Detaches the callback function from a Timer object
+ **Syntax**
    void detachInterrupt()
+ **Parameters**
    none
+ **Return**
    none
+ **Usage**
    TL_Timer.detachInterrupt()
    ***or***
    TL_Timer1.detachInterrupt()
    ***or***
    TL_Timer2.detachInterrupt()
    ………
    ***or***
    TL_Timern.detachInterrupt()
    (Note: n is a numberic that is less than 8 and we provide 8 software timers for users )
+ **Example**
```c++
// Print the times the timer expires in a interval of 1s up to 20
int i = 0;
void callback() {
    TL_Serial.println("Timer expires " + String(i++) + "times");
}
void callback1() {
    TL_Serial.println("New callback function! Timer expires " + String(i++) +  "times");
}
void setup() {
    TL_Serial.begin(9600);
    // Set the period and the type of the timer
    TL_Timer.setPeriod(1000, TIMER_PERIODIC);
    // Attach the callback function to the timer. When the timer expires, the callback function will be excuted
    TL_Timer.attachInterrupt(callback);
    // Start the timer
    TL_Timer.start();
    TL_Time.delayMillis(10000);
    TL_Timer.detachInterrupt();
    TL_Timer.attachInterrupt(callback1);
    TL_Time.delayMillis(10000);
    //Stop the timer
    TL_Timer.stop();
}

void loop() {
}
```

#### setPeriod()
+ **Description**
    Sets the period(in milliseconds) and the type of a Timer object, e.g. TIMER_ONE_SHOT(expiring just once), TIMER_PERIODIC(repeatedly expiring after the initial expiration). A timer can be set more than once.
+ **Syntax**
    void setPeriod(unsigned long ms, int type = TIMER_PERIODIC)
+ **Parameters**
    **ms**: the period in millisecond of the timer
    **type**: the type of the timer, which can only be TIMER_ONE_SHOT(0) or TIEMR_PERIODIC(1)   and the type defaults to TIMER_PERIODIC
+ **Return**
    none
+ **Usage**
    TL_Timer.setPeriod(ms, type)
    ***or***
    TL_Timer1.setPeriod(ms, type)
    ***or***
    TL_Timer2.setPeriod(ms, type)
    ………
    ***or***
    TL_Timern.setPeriod(ms, type)
    (Note: n is a numberic that is less than 8 and we provide 8 software timers for users )
+ **Example**
```c++
// Print the times the timer expires in a interval of 1s up to 10
int i = 0;
void callback() {
    TL_Serial.print("Timer expires " + String(i++) + "times");
}
void setup() {
    TL_Serial.begin(9600);
    // Set the period and the type of the timer
    TL_Timer.setPeriod(1000, TIMER_PERIODIC);
    // Attach the callback function to the timer. When the timer expires, the callback function will be excuted
    TL_Timer.attachInterrupt(callback);
    // Start the timer
    TL_Timer.start();
    TL_Time.delayMillis(10000);
    //Stop the timer
    TL_Timer.stop();
}

void loop() {
}
```


#### setFrequency()
+ **Description**
    Sets the frequency (in Hz) and the type of a Timer, e.g. TIMER_ONE_SHOT(expiring just once), TIMER_PERIODIC(repeatedly expiring after the initial expiration). A timer can be set more than once.
+ **Syntax**
    void setFrequency(unsigned long freq, int type = TIMER_PERIODIC)
+ **Parameters**
    **freq**: the frequency of the timer
    **type**: the type of the timer, which can only be TIMER_ONE_SHOT(0)or TIEMR_PERIODIC(1)     and the type defaults to TIMER_PERIODIC
+ **Return**
    none
+ **Usage**
    TL_Timer.setFrequency(frep, type)
    ***or***
    TL_Timer1.setFrequency(frep, type)
    ***or***
    TL_Timer2.setFrequency(frep, type)
    ………
    ***or***
    TL_Timern.setFrequency(frep, type)
    (Note: n is a numberic that is less than 8 and we provide 8 software timers for users)
+ **Example**
```c++
// Print the times the timer expires in a interval of 1s up to 10
int i = 0;
void callback() {
    TL_Serial.print("Timer expires " + String(i++) + "times");
}
void setup() {
    TL_Serial.begin(9600);
    TL_Timer.setFrequency(1, TIMER_PERIODIC);
    // Attach the callback function to the timer. When the timer expires, the callback function will be excuted
    TL_Timer.attachInterrupt(callback);
    // Start the timer
    TL_Timer.start();
    TL_Time.delayMillis(10000);
    //Stop the timer
    TL_Timer.stop();
}

void loop() {
}
```


## TL_Storage library
The TL_Storage library allows for reading from and writing to external SD card storage/internal specific files area. 
For Arduino UNO and LinkIt One, the communication between the microcontroller and the SD card uses SPI. 
For Raspberry and BeagleBone Black, a specific files areas (e.g. */SD_MOCK) is created internally and perform read and write operations similar to SD card.

### Storage Module
The storage module provides functions for accessing the storage area and manipulating its files and directories.
#### begin()
+ **Description**
    Initializes the storage module. The initialization is necessasy before using the stroage module
+ **Syntax**
    bool begin()
+ **Parameters**
    none
+ **Return**
    **bool**: true on success; false on failure 
+ **Usage**
    TL_Storage.begin()

#### open()
+ **Description**
    Opens a file in the storage
+ **Syntax**
    TL_File open(const String &filepath)
    TL_File open(const char \*filepath)
    TL_File open(const String &filepath, String &mode = “r”)
    TL_File open(const char \*filepath, const char *mode = “r”)
+ **Parameters**
    **filepath**: the name the file to open.The filepath is a relative file path.
    **mode(optional)**: the mode in which to open the file, defaults to read( “r” ). Valid values are
---------------------------------------------------------------
| File access mode string |    Meaning     |               Explanation                | Action if file already exists | Action if file does not exist |
| :---------------------- | :------------: | :--------------------------------------: | :---------------------------: | :---------------------------: |
| "r"                     |      read      | Open a file for reading at the beginning of the file |        read from start        |        failure to open        |
| "w"                     | write and read | Create a file for writing and reading starting at the start of the file |       destroy contents        |          create new           |

+ **Return**
    **TL_File**: a File object referring to the opened file; if the file couldn't be opened, this object will evaluate to false in a boolean context, i.e. you can test the return value with "if (f)". More details about the File type, please refer to the next File Module
+ **Usage**
    TL_Storage.open(filepath)
    ***or***
    TL_Storage.open(filepath, mode)
+ **Example**
```c++
void setup() {
    TL_Serial.begin(9600);
    TL_Storage.begin();
    TL_File fp = TL_Storage.open("1.txt", "r");
    if(fp) {
        TL_Serial.println("Open the 1.txt successfully");
    }
    // other codes
    ...
}

void loop() {
}
```

#### exists()
+ **Description**
    Checks whether a file or directory exists in the storage module. 
+ **Syntax**
    bool exists(cosnt char *filepath)   
    bool exists(const String &filepath)
+ **Parameters**
    **filepath**: the name the file/directory to check for existence and the file path is a relative path, e.g exist(“a.txt”), exist(“1/2/3”)
+ **Return**
    **bool**: true means existing; false means not existing
+ **Usage**
    TL_Storage.exists(filepath)
+ **Example**
```c++
void setup() {
    TL_Serial.begin(9600);
    TL_Storage.begin();
    if(TL_Storage.exists("1.txt")) {
        TL_Serial.println("The file 1.txt exists");
    }
    if(TL_Storage.exists("1/2/3")) {
        TL_Serial.println("The directory 1/2/3 exists");
    }
}

void loop() {
}
```


#### mkdir()
+ **Description**
    Creates a directory in the storage module. This will also create any intermediate directories that don't already exists; e.g. TL_Storage.mkdir("a/b/c") will create a, b, and c
+ **Syntax**
    bool mkdir(const char *filepath)
    bool mkdir(cosnt string &filepath)
+ **Parameters**
    **filepath**: the name of the directory to create, with sub-directories separated by forward-slashes, “/”. The filepath is a relative file path.
+ **Return**
    **bool**: true if the creation of the directory succeeded, false if not
+ **Usage**
    TL_Storage.mkdir(filepath)
+ **Example**
```c++
void setup() {
    TL_Storage.begin();
    if(TL_Storage.mkdir("1/2/4")) {
        TL_Serial.println("Create the directory successfully");
    }
}

void loop() {
}
```

#### remove()
+ **Description**
    Removes a file from the external storage.
+ **Syntax**
    bool remove(const char *filename)
    bool remove(const String &filename)
+ **Parameters**
    **filename**: the name of the file to remove, with sub-directories separated by forward- slashes, "/".The filepath is a relative file path.
+ **Return**
    **bool**: true on success; false on failure
+ **Usage**
    TL_Storage.remove(filepath)
+ **Example**
```c++
void setup() {
    TL_Storage.begin();
    if(TL_Storage.remove("1.txt")) {
        TL_Serial.println("Remove the file successfully");
    }
}

void loop() {
}
```


#### rmdir()
+ **Description**
    Removes a directory from the external storage. The directory must be empty
+ **Syntax**
    bool remove(cosnt char *filepath)
    bool remove(const String &filepath)
+ **Parameters**
    **filepath**: the name of the directory to remove, with sub-directories separated by forward-slashes, /The filepath is a relative file path.
+ **Return**
    **bool**: true on success; false on failure
+ **Usage**
    TL_Storage.rmdir(filepath)
+ **Example**
```c++
void setup() {
    TL_Storage.begin();
    if(TL_Storage.rmdir("1/2/4")) {
        TL_Serial.println("Remove the directory successfully");
    }
}

void loop() {
}
```


### File Module
The File module allows for reading from and writing to individual files on the storage area.

#### close()
+ **Description**
    Closes the file, and ensure that any data written to it is physically saved to the storage.
+ **Syntax**
    bool close()
+ **Parameters**
    none
+ **Return**
    **int**: true on success; false on failure
+ **Usage**
    TL_File fp = TL_Storage.open(filepath, mode);
    …..
    fp.close(); 
    (Note: TL_File is a artificial Module and you can declare and define objects of TL_File type)
+ **Example**
```c++
void setup() {
    TL_Serial.begin(9600);
    TL_Storage.begin();
    TL_File fp = TL_Storage.open("1.txt", "r");
    if(fp) {
        TL_Serial.println("Open the 1.txt successfully");
    }
    // other codes
    ...
    // Close the file
    fp.close();
}

void loop() {
}
```


#### read()
+ **Description**
    Reads one byte from the file return it or reads some bytes from the file and stores them in the buffer
+ **Syntax**
    int read()
    int read(char* buf, int size)
+ **Parameters**
    **buf**: an array of characters or bytes where the reading bytes are stored
    **size**: the number of bytes read from the file
+ **Return**
    **int**: for call with no parameters, the return value is the obtained byte and for call with two parameters, the return value the number of bytes read, which may be less than size if an error or end-of-file condition occurs
+ **Usage**
    TL_File fp = TL_Storage.open(filepath, mode);
    …… 
    int ch = fp.read();
    ***or*** 
    TL_File fp = TL_Storage.open(filepath, mode);
    ……
    int ch = fp.read(buf, size);
    (Note: TL_File is a artificial Module and you can declare and define objects of TL_File type)
+ **Example**
```c++
void setup() {
    TL_Serial.begin(9600);
    TL_Storage.begin();
    TL_File fp = TL_Storage.open("1.txt", "r");
    if(!fp) {
        TL_Serial.println("Opening the 1.txt fails");
        return;
    }
    // Read a character from the file
    char comingByte = fp.read();
    TL_Serial.print("Reading byte is ");
    TL_Serial.println(comingByte);
    char buf[10];
    // Read a array of characters from the file
    fp.read(buf, 10);
    TL_Serial.print("Reading bytes are ");
    TL_Serial.println(buf);
    // Close the file
    fp.close();
}

void loop() {
}
```


#### write()
+ **Description**
    writes data to the file; returns the number of bytes written
+ **Syntax**
    int write(const char data)
    int write(const char* buf)
    int write(const String& buf)
+ **Parameters**
    **data**: the char to write
    **buf**: an array of characters or bytes
+ **Return**
    **int**: the number of bytes written, though reading that number is optional
+ **Usage**
    TL_File fp = TL_Storage.open(filepath, mode);
    …… 
    fp.write(data);
    ***or***
    TL_File fp = TL_Storage.open(filepath, mode);
    …… 
    fp.write(data, size);
    (Note: TL_File is a artificial Module and you can declare and define objects of TL_File type)
+ **Example**
```c++
void setup() {
    TL_Serial.begin(9600);
    TL_Storage.begin();
    TL_File fp = TL_Storage.open("2.txt", "w");
    if(!fp) {
        TL_Serial.println("Opening the 2.txt fails");
        return;
    }
    fp.write('1');
    fp.write("23");
    String str("4567");
    fp.write(str);
    fp.close();

}

void loop() {
}
```


#### flush()
+ **Description**
    Ensures that any bytes written to the file are physically saved to the  storage area. This is done automatically when the file is closed.
+ **Syntax**
    void flush()
+ **Parameters**
    none
+ **Return**
    none
+ **Usage**
    TL_File fp = TL_Storage.open(filepath, mode);
    …… 
    fp.write(data);
    fp.flush();
    (Note: TL_File is a artificial Module and you can declare and define objects of TL_File type)
+ **Example**
```c++
void setup() {
    TL_Serial.begin(9600);
    TL_Storage.begin();
    TL_File fp = TL_Storage.open("2.txt", "w");
    if(!fp) {
        TL_Serial.println("Opening the 2.txt fails");
        return;
    }
    fp.write('1');
    fp.write("23");
    String str("4567");
    fp.write(str);
    fp.flush();
    fp.close();

}

void loop() {
}
```


#### position()
+ **Description**
    Gets the current position of the file pointer
+ **Syntax**
    unsigned long position()
+ **Parameters**
    none
+ **Return**
    **long**: the position of the file pointer
+ **Usage**
    TL_File fp = TL_Storage.open(filepath, mode);
    …..
    long pos = fp.position(); 
    (Note: TL_File is a artificial Module and you can declare and define objects of TL_File type)
+ **Example**
```c++
void setup() {
    TL_Serial.begin(9600);
    TL_Storage.begin();
    TL_File fp = TL_Storage.open("2.txt", "w");
    if(!fp) {
        TL_Serial.println("Opening the 2.txt fails");
        return;
    }
    fp.write("123");
    fp.close();
    fp = TL_Storage.open("2.txt", "r");
    fp.read();
    long cur_pos = fp.position();
    TL_Serial.print("The current position of the file pointer is");
    TL_Serial.println(cur_pos);
    char comingByte = fp.read();
    TL_Serial.print("The reading character is ");
    TL_Serial.println(comingByte);
    fp.close();
}

void loop() {
}
```


#### seek()
+ **Description**
    Shifts the file pointer for a offset distance relative to the beginning of the file
+ **Syntax**
    int seek(long offset)
+ **Parameters**
    **offset**: number of characters to shift the file pointer relative to the beginning of the file
+ **Return**
    **int**: 0 on success, nonzero value otherwise
+ **Usage**
    TL_File fp = TL_Storage.open(filepath, mode);
    …..
    fp.seek(offset); 
    (Note: TL_File is a artificial Module and you can declare and define objects of TL_File type)
+ **Example**
```c++
void setup() {
    TL_Serial.begin(9600);
    TL_Storage.begin();
    TL_File fp = TL_Storage.open("2.txt", "w");
    if(!fp) {
        TL_Serial.println("Opening the 2.txt fails");
        return;
    }
    fp.write("123");
    fp.close();
    fp = TL_Storage.open("2.txt", "r");
    fp.read();
    long cur_pos = fp.position();
    TL_Serial.print("The current position of the file pointer is");
    TL_Serial.println(cur_pos);
    fp.seek(cur_pos + 1);
    char comingByte = fp.read();
    TL_Serial.print("The reading character is ");
    TL_Serial.println(comingByte);
    fp.close();
}

void loop() {
}
```

#### size()
+ **Description**
    Gets the size of the file
+ **Syntax**
    unsigned long size()
+ **Parameters**
    none
+ **Return**
    **unsigned long**: the size of the file in bytes
+ **Usage**
    TL_File fp = TL_Storage.open(filepath, mode);
    …..
    unsigned longf_size = fp.size(); 
    (Note: TL_File is a artificial Module and you can declare and define objects of TL_File type)

# Extended API

## TL_WiFi library
The TL_WiFi library allows for initializing the WiFi hardare and network setting.
### WiFi Module

#### init()
+ **Description**
    Initializes the WiFi hardware module. Initialization is necassary before using Wifi module
+ **Syntax**
    bool init()
+ **Parameters**
    none
+ **Return**
    **bool**: true on success; false on failure
+ **Usage**
    TL_WiFi.init()

#### join()
+ **Description**
    Connects to the router named with the SSID; Return true on success or false on failure
+ **Syntax**
    void join(cosnt char \*SSID, const char \*PassW = "")
    void join(cosnt String &SSID, const String &PassW = "")
+ **Parameters**
    **SSID**: the SSID of the router  
    **PassW**: the password of the router
+ **Return**
    **bool**: true on success; false on failure
+ **Usage**
    TL_WiFi.join(SSID)
    ***or****
    TL_WiFi.join(SSID, PassW)
+ **Example**
```c++
void setup() {
    TL_Serial.begin(9600);
    bool a = TL_WiFi.init();
    if(a) {
        TL_Serial.println("WiFi module initialization succeeds");
    }
    else {
        TL_Serial.println("WiFi module initialization fails");
    }
    bool b = TL_WiFi.join("SSID", "PassW");
    if(b) {
        TL_Serial.println("Joining the Wifi networks succeeds");
    }
    else {
        TL_Serial.println("Joining the Wifi networks fails");
    }
}

void loop() {
}
```

#### disjoin()
+ **Description**
    Disconnects from the router; Return true on success or false on failure
+ **Syntax**
    bool disjoin()
+ **Parameters**
    none
+ **Return**
    **bool**: true on success; false on failure
+ **Usage**
    TL_WIFI.disjoin(SSID)
+ **Example**
```c++
void setup() {
    TL_Serial.begin(9600);
    bool a = TL_WiFi.init();
    if(a) {
        TL_Serial.println("WiFi module initialization succeeds");
    }
    else {
        TL_Serial.println("WiFi module initialization fails");
    }
    bool b = TL_WiFi.join("SSID", "PassW");
    if(b) {
        TL_Serial.println("Joining the Wifi networks succeeds");
    }
    else {
        TL_Serial.println("Joining the Wifi networks fails");
    }
    bool c = TL_WiFi.disjoin();
    if(c) {
        TL_Serial.println("Disjoining the Wifi networks succeeds");
    }
    else {
        TL_Serial.println("Disjoining the Wifi networks fails");
    }
}

void loop() {
}
```

#### fetchHTTP()
+ **Description**
    Fetch a HTTP client from the WiFi module that can send and receive data through HTTP protocol.
+ **Syntax**
    TL_HTTP fetchHTTP()
+ **Parameters**
    none
+ **Return**
    **TL_HTTP**: a HTTP client object built from the WiFi network. More details about the TL_HTTP type, please refer to the TL_HTTP library.
+ **Usage**
    TL_WiFi.fetchHTTP()
+ **Example**
```c++
void setup() {
    TL_Serial.begin(9600);
    bool a = TL_WiFi.init();
    if(a) {
        TL_Serial.println("WiFi module initialization succeeds");
    }
    else {
        TL_Serial.println("WiFi module initialization fails");
    }
    bool b = TL_WiFi.join("SSID", "PassW");
    if(b) {
        TL_Serial.println("Joining the Wifi networks succeeds");
    }
    else {
        TL_Serial.println("Joining the Wifi networks fails");
    }
    // fetch a MQTT client from the WiFi network
    TL_HTTP http_client = TL_WiFi.fetchHTTP();
    // other codes
    ...
}

void loop() {
}
```

#### fetchMQTT()
+ **Description**
    Fetch a MQTT client from the WiFi module that can subscirbe and publish topics through MQTT protocol.
+ **Syntax**
    TL_MQTT fetchMQTT()
+ **Parameters**
    none
+ **Return**
    **TL_MQTT**: a MQTT client object built from the WiFi network. More details about the TL_MQTT type, please refer to the TL_MQTT library.
+ **Usage**
    TL_WiFi.fetchMQTT()
+ **Example**
```c++
void setup() {
    TL_Serial.begin(9600);
    bool a = TL_WiFi.init();
    if(a) {
        TL_Serial.println("WiFi module initialization succeeds");
    }
    else {
        TL_Serial.println("WiFi module initialization fails");
    }
    bool b = TL_WiFi.join("SSID", "PassW");
    if(b) {
        TL_Serial.println("Joining the Wifi networks succeeds");
    }
    else {
        TL_Serial.println("Joining the Wifi networks fails");
    }
    // fetch a MQTT client from the WiFi network
    TL_MQTT mqtt_client = TL_WiFi.fetchMQTT();
    // other codes
    ...
}

void loop() {
}
```

## TL_HTTP library
The TL_HTTP library provides the basic functions of Http protocol.

### HTTP_Client module

#### get()
+ **Description**
    Request data from a specified resource(e.g., URL) via HTTP method
+ **Syntax**
    bool get(const char\* url)
    bool get(const String& url)
+ **Parameters**
    **url**: the URL of resource, e.g., "http://host[:port]/path"
+ **Return**
    **bool**: true on success; false on failure
+ **Usage**
    TL_HTTP http_client = TL_WiFi.fetchHTTP()
    ...
    http_client.get(url)
+ **Example**
```c++
String url("http://10.214.149.119/tinylink/receiveData.php?userid=UserID&nodeid=NodeID&temperature=");
void setup() {
    TL_Serial.begin(9600);
    bool a = TL_WiFi.init();
    if(a) {
        TL_Serial.println("WiFi module initialization succeeds");
    }
    else {
        TL_Serial.println("WiFi module initialization fails");
    }
    bool b = TL_WiFi.join("SSID", "PassW");
    if(b) {
        TL_Serial.println("Joining the Wifi networks succeeds");
    }
    else {
        TL_Serial.println("Joining the Wifi networks fails");
    }
    TL_HTTP http_client = TL_WiFi.fetchHTTP();
}

void loop() {
    TL_Temperature.read();
    http_client.get(url + String(TL_Temperature.data()));
    TL_Time.delayMillis(1000);
}
```

#### post()
+ **Description**
    Submits data to be processed to a specified resource (e.g., URL) via HTTP POST method
+ **Syntax**
    bool post(const String &url, const String &data)
    bool post(const char\* url, const char\* data)
+ **Parameters**
    **url**: the URL of the resource
    **data**: the content to post to the remote host and the format of data must be of the specific format, e.g. name=xxx&age=xxx
+ **Return**
    **bool**: true on success; false on failure
+ **Usage**
    TL_HTTP http_client = TL_WiFi.fetchHTTP()
    ...
    http_client.post(url, data)
+ **Example**
```c++
String url("http://10.214.149.119/tinylink/receiveData.php");
void setup() {
    TL_Serial.begin(9600);
    bool a = TL_WiFi.init();
    if(a) {
        TL_Serial.println("WiFi module initialization succeeds");
    }
    else {
        TL_Serial.println("WiFi module initialization fails");
    }
    bool b = TL_WiFi.join("SSID", "PassW");
    if(b) {
        TL_Serial.println("Joining the Wifi networks succeeds");
    }
    else {
        TL_Serial.println("Joining the Wifi networks fails");
    }
    TL_HTTP http_client = TL_WiFi.fetchHTTP();
}

void loop() {
    TL_Temperature.read();
    TL_Humidity.read();
    http_client.post(url, String("userid=UserID")+"&"+"nodeid=NodeID"+"&"+"temperature=" + String(TL_Temperature.data()) + "&" + "humidity=" + String(TL_Humidity.data()));
    TL_Time.delayMillis(1000);
}
```

#### getResponse()
+ **Description**
    Get the data returned form the HTTP Post or Get request.
+ **Syntax**
    const String& getResponse()
+ **Parameters**
    none
+ **Return**
    **const String&**: the response string get from the Post/Get request
+ **Usage**
    TL_HTTP http_client = TL_WiFi.fetchHTTP()
    ...
    http_client.post(url, data)
    String res = http_client.getResponse()
    ***or***
    TL_HTTP http_client = TL_WiFi.fetchHTTP()
    ...
    http_client.get(url)
    String res = http_client.getResponse()
+ **Example**
```c++
String url("http://10.214.149.119/tinylink/receiveData.php?userid=UserID&nodeid=NodeID&temperature=");
void setup() {
    TL_Serial.begin(9600);
    bool a = TL_WiFi.init();
    if(a) {
        TL_Serial.println("WiFi module initialization succeeds");
    }
    else {
        TL_Serial.println("WiFi module initialization fails");
    }
    bool b = TL_WiFi.join("SSID", "PassW");
    if(b) {
        TL_Serial.println("Joining the Wifi networks succeeds");
    }
    else {
        TL_Serial.println("Joining the Wifi networks fails");
    }
    TL_HTTP http_client = TL_WiFi.fetchHTTP();
    TL_Temperature.read();
    http_client.get(url + String(TL_Temperature.data()));
    String res = http_client.getResponse();
    TL_Serial.println(res);
}

void loop() {
}
```

## TL_MQTT library
The TL_MQTT library provides the basic functions of MQTT protocol.

### MQTT_Client module

#### connnect()
+ **Description**
    Connecs to a remote server with specified options(Sends an MQTT connection packet). After execution, all connection options are stored internally for 
+ **Syntax**
    int connect(const String& serverName, int port, const String& clientName, const String& userName= "", const String& passW = "")
    int connect(const char\* serverName, int port, const char\* clientName, const char\* userName= "", const char\* passW= "")
+ **Parameters**
    **severName**: the hostname of the remote server
    **port**: the port number
    **clientName**: the clientID
    **userName**：the username
    **passW**: the password of the user
+ **Return**
    **int**: 0 if successes, nonzero value otherwise
+ **Usage**
    TL_MQTT mqtt_client = TL_WiFi.fetchMQTT()
    ...
    mqtt_client.connect(serverName, port, clientName)
    ***or***
    TL_MQTT mqtt_client = TL_WiFi.fetchMQTT()
    ...
    mqtt_client.connect(serverName, port, clientName, userName, passW)
+ **Example**

#### reconnect()
+ **Description**
    Reconnects to the remote server with previously stored connection options(Sends an MQTT connection packet again)
+ **Syntax**
    int reconnect()
+ **Parameters**
    none
+ **Return**
    **int**: 0 if successes, nonzero value otherwise
+ **Usage**
    TL_MQTT mqtt_client = TL_WiFi.fetchMQTT()
    ...
    mqtt_client.connect(serverName, port, clientName)
    ...
    mqtt_client.reconnnect()
+ **Example**

#### disconnect()
+ **Description**
    Disconnect to the remote server that the client previously connected to and clear up all state(Sends an MQTT disconnection packet)
+ **Syntax**
    int disconnect()
+ **Parameters**
    none
+ **Return**
    **int**: 0 if successes, nonzero value otherwise
+ **Usage**
    TL_MQTT mqtt_client = TL_WiFi.fetchMQTT()
    ...
    mqtt_client.connect(serverName, port, clientName)
    ...
    mqtt_client.disconnnect()
+ **Example**

#### isConnected()
+ **Description**
    Check whether the client and server are still connectiong to each other
+ **Syntax**
    bool isConnected()
+ **Parameters**
    none
+ **Return**
    **bool**: ture if connected, false otherwise
+ **Usage**
    TL_MQTT mqtt_client = TL_WiFi.fetchMQTT()
    ...
    mqtt_client.connect(serverName, port, clientName)
    ...
    if(mqtt_client.isConnected()) {
        ...
    }
+ **Example**

#### publish()
+ **Description**
    Sends a message to the client/server(Sends an MQTT publish packet)

+ **Syntax**
    int publish(const String& topicName, const String& data, int length, int qos = 0<!---, bool retained = false-->)
    int publish(const char\* topicName, const char\* data, int length, int qos = 0<!---, bool retained = false-->)

    <!-- int publish(const char\* topicName, const char\* data, unsigned short& id, int qos = 1, bool retained = false) int publish(const String& topicName, const String& data, unsigned short& id, int qos = 1) -->

+ **Parameters**
    **topicName**: the topic to be published
    **data**: the concrete content of the sent message
    **length**: the length of sent message
    **qos**: the QoS to send the data at. Valid value is 0,1,2(Larger value means better quality of service).
    <!---**id**: the packet id--><!---**retianed**: whether the message should be retained-->
+ **Return**
    **int**: 0 if successes, nonzero value otherwise

+ **Usage**
    TL_MQTT mqtt_client = TL_WiFi.fetchMQTT();
    ...
    mqtt_client.connect(serverName, port, clientName);
    ...
    mqtt_client.publish(topicName, data, qos, retained);
    ***or***
    TL_MQTT mqtt_client = TL_WiFi.fetchMQTT();
    ...
    mqtt_client.connect(serverName, port, clientName);
    ...
    mqtt_client.publish(topicName, data, id, qos, retained);

+ **Example**
```
const char* hostname = "grf0a9.messaging.internetofthings.ibmcloud.com";
int port = 1883;
const char* clientID = "d:grf0a9:fkb_Humi:test_1";
const char* userName = "use-token-auth";
const char* passW = "123456789";
const char* topic = "iot-2/evt/eventid1/fmt/json";

void setup() {
    TL_Serial.begin(9600);
    bool a = TL_WiFi.init();
    if(a) {
        TL_Serial.println("WiFi module initialization succeeds");
    }
    else {
        TL_Serial.println("WiFi module initialization fails");
    }
    bool b = TL_WiFi.join("SSID", "PassW");
    if(b) {
        TL_Serial.println("Joining the Wifi networks succeeds");
    }
    else {
        TL_Serial.println("Joining the Wifi networks fails");
    }
    TL_MQTT mqtt_client = TL_WiFi.fetchMQTT();
    TL_Serial.println("MQTT begin connecting");
    mqtt_Client.connect(hostname, port, clientID, userName, passW);
    TL_Serial.println(String("the status of connection is ") +  mqtt_Client.isConnected());
    float light = 100;
    char buf[100];
    for(int i = 0; i < 5; i++) {
        sprintf(buf, "{\"Light\": %f}", light + 1);
        mqtt_Client.publish(topic, buf);      
    }
}

void loop() {
}
```

#### subscribe()
+ **Description**
    Subscribe a topic(Sends an MQTT subscribe packet)
+ **Syntax**
    int subscribe(const String& topicName, void (\*callback)(MessageData& md), int qos = 0)
    int subscribe(const char\* topicName, void (\*callback)(MessageData& md), int qos = 0)
+ **Parameters**
    **topicName**: the topic to be subscribed
    **callback**: the callback function to be invoked when a message is received for this subscription
    ***Note***: **MessageData** is actually a structure in Paho project, an open-source client implemetation of MQTT and MQTT-SN messaging protocols. More details, please refer to [MQTTCLient.h](https://github.com/eclipse/paho.mqtt.embedded-c/blob/master/MQTTClient/src/MQTTClient.h)
    **qos**: the QoS to subscribe at. Valid value is 0,1,2(Larger value means better quality of service).
+ **Return**
    **int**: 0 if successes, nonzero value otherwise
+ **Usage**
    TL_MQTT mqtt_client = TL_WiFi.fetchMQTT();
    ...
    mqtt_client.connect(serverName, port, clientName);
    ...
    mqtt_client.subscribe(topicFilter, callback, qos);
+ **Example**
```
const char* hostname = "grf0a9.messaging.internetofthings.ibmcloud.com";
int port = 1883;
const char* clientID = "d:grf0a9:fkb_Humi:test_1";
const char* userName = "use-token-auth";
const char* passW = "123456789";
const char* topic = "iot-2/evt/eventid1/fmt/json";
void messageArrived(MQTT::MessageData& md){
    MQTT::Message &message = md.message;
	printf("Message arrived: qos %d, packetid %d\n", message.qos, message.id);
    printf("Payload %.*s\n", (int)message.payloadlen, (char*)message.payload);
}
void setup() {
    TL_Serial.begin(9600);
    bool a = TL_WiFi.init();
    if(a) {
        TL_Serial.println("WiFi module initialization succeeds");
    }
    else {
        TL_Serial.println("WiFi module initialization fails");
    }
    bool b = TL_WiFi.join("SSID", "PassW");
    if(b) {
        TL_Serial.println("Joining the Wifi networks succeeds");
    }
    else {
        TL_Serial.println("Joining the Wifi networks fails");
    }
    TL_MQTT mqtt_client = TL_WiFi.fetchMQTT();
    TL_Serial.println("MQTT begin connecting");
    mqtt_Client.connect(hostname, port, clientID, userName, passW);
    TL_Serial.println(String("the status of connection is ") +  mqtt_Client.isConnected());
	mqtt_Client.subscribe(topic, messageArrived, 0);
}

void loop() {
}
```

#### ubsubscribe()
+ **Description**
    Unsubscribe a topic(Sends an MQTT unsubscribe packet)
+ **Syntax**
    int unsubscribe(const String& topicName)
    int unsubscribe(const char* topicName)
+ **Parameters**
    **topicName**: the topic to be unsubscribed
+ **Return**
    **int**: 0 if successes, nonzero value otherwise
+ **Usage**
    TL_MQTT mqtt_client = TL_WiFi.fetchMQTT()
    ...
    mqtt_client.connect(serverName, port, clientName)
    ...
    mqtt_client.unsubscribe(topicFilter)
+ **Example**
```
const char* hostname = "grf0a9.messaging.internetofthings.ibmcloud.com";
int port = 1883;
const char* clientID = "d:grf0a9:fkb_Humi:test_1";
const char* userName = "use-token-auth";
const char* passW = "123456789";
const char* topic = "iot-2/evt/eventid1/fmt/json";
void messageArrived(MQTT::MessageData& md){
    MQTT::Message &message = md.message;
	printf("Message arrived: qos %d, packetid %d\n", message.qos, message.id);
    printf("Payload %.*s\n", (int)message.payloadlen, (char*)message.payload);
}
void setup() {
    TL_Serial.begin(9600);
    bool a = TL_WiFi.init();
    if(a) {
        TL_Serial.println("WiFi module initialization succeeds");
    }
    else {
        TL_Serial.println("WiFi module initialization fails");
    }
    bool b = TL_WiFi.join("SSID", "PassW");
    if(b) {
        TL_Serial.println("Joining the Wifi networks succeeds");
    }
    else {
        TL_Serial.println("Joining the Wifi networks fails");
    }
    TL_MQTT mqtt_client = TL_WiFi.fetchMQTT();
    TL_Serial.println("MQTT begin connecting");
    mqtt_Client.connect(hostname, port, clientID, userName, passW);
    TL_Serial.println(String("the status of connection is ") +  mqtt_Client.isConnected());
	mqtt_Client.subscribe(topic, messageArrived, 0);
	mqtt_Client.unsubscribe(topic);
}

void loop() {
}
```

## TL_LED Library
The TL_LED library provides some basic controlling methods for leds.

### Led Module

#### turnOn()
+ **Description**
    Turns on the led
+ **Syntax**
    void turnOn()
+ **Parameters**
    none
+ **Return**
    none
+ **Usage**
    TL_LED.turnOn()

#### turnOff()
+ **Description**
    Turns off the led
+ **Syntax**
    void turnOff()
+ **Parameters**
    none
+ **Return**
    none
+ **Usage**
    TL_LED.turnOff()
+ **Example**
```c++
void setup() {
}

void loop() {
    TL_LED.turnOn();
    TL_Time.delayMillis(1000);
    TL_LED.turnOff();
    TL_Time.delayMillis(1000);
}
```

#### toggle()
+ **Description**
    Toggles the state of the led. If the led is on, turn off it and if the led is off, turn on the led
+ **Syntax**
    void toggle()
+ **Parameters**
    none
+ **Return**
    none
+ **Usage**
    TL_LED.toggle
+ **Example**
```c++
void setup() {
}

void loop() {
    TL_LED.toggle();
    TL_Time.delayMillis(1000);
}
```

## Air quality sensorlibrary
The air quality sensor library provides some basic functions for PM25 sensors.

### PM25 Module

#### read()
+ **Description**
    Reads PM25 data once from the sensor and stores it in the buffer.(the reading operation isblocking)
+ **Syntax**
    void read()
+ **Parameters**
    none
+ **Return**
    **int**: 0 if successes, nonzero value otherwise
+ **Usage**
    TL_PM25.read()

#### data()
+ **Description**
    Reads PM25 data from the buffer
+ **Syntax**
    double data()
+ **Parameters**
    none
+ **Return**
    **double**: PM25 data stored in the buffer
+ **Usage**
    TL_PM25.data()
+ **Example**
```c++
void setup() {
    TL_Serial.begin(9600);
}

void loop() {
    TL_Time.delayMillis(1000);
    TL_PM25.read();
    TL_Serial.print("PM25 data is ");
    TL_Serial.println(TL_PM25.data());    
}
```

## Temperature and humidity sensor library
The temperature and humidity sensor library provides some basic functions for temperature sensor and humidity sensor.

### Humidity Module

#### read()
+ **Description**
    Reads humidity data once from the sensor and stores it in the buffer.(the reading operation isblocking)
+ **Syntax**
    void read()
+ **Parameters**
    none
+ **Return**
    **int**: 0 if successes, nonzero value otherwise
+ **Usage**
    TL_Humidity.read()

#### data()
+ **Description**
    Reads humidity data from the buffer
+ **Syntax**
    double data()
+ **Parameters**
    none
+ **Return**
    **double**: humidity data stored in the buffer
+ **Usage**
    TL_Humidity.data()
+ **Example**
```c++
void setup() {
    TL_Serial.begin(9600);
}

void loop() {
    TL_Time.delayMillis(1000);
    TL_Humidity.read();
    TL_Serial.print("Humidity data is ");
    TL_Serial.println(TL_Humidity.data());    
}
```

### Temperature Module

#### read()
+ **Description**
    Reads temperature data once from the sensor and stores it in the buffer.(the reading operation isblocking)
+ **Syntax**
    void read()
+ **Parameters**
    none
+ **Return**
    **int**: 0 if successes, nonzero value otherwise
+ **Usage**
    TL_Temperature.read()

#### data()
+ **Description**
    Reads temperature data from the buffer
+ **Syntax**
    double data()
+ **Parameters**
    none
+ **Return**
    **double**: temperature data stored in the buffer
+ **Usage**
    TL_Temperature.data()
+ **Example**
```c++
void setup() {
    TL_Serial.begin(9600);
}

void loop() {
    TL_Time.delayMillis(1000);
    TL_Temperature.read();
    TL_Serial.print("Temperature data is ");
    TL_Serial.println(TL_Temperature.data());    
}
```

## Soil Humidity sensor library
The light sensor library provides some basic functions for light sensor.

### Soil_Humidity Module

#### read()
+ **Description**
    Reads soil humidity data once from the sensor and stores it in the buffer.(the reading operation isblocking)
+ **Syntax**
    void read()
+ **Parameters**
    none
+ **Return**
    **int**: 0 if successes, nonzero value otherwise
+ **Usage**
    TL_Soil_Humidity.read()

#### data()
+ **Description**
    Reads soil humidity data from the __buffer__
+ **Syntax**
    double data()
+ **Parameters**
    none
+ **Return**
    **double**: soil humidity data stored in the buffer
+ **Usage**
    TL_Soil_Humidity.data()
+ **Example**
```c++
void setup() {
    TL_Serial.begin(9600);
}

void loop() {
    TL_Time.delayMillis(1000);
    TL_Soil_Humidity.read();
    TL_Serial.print("Soil_Humidity data is ");
    TL_Serial.println(TL_Soil_Humidity.data());    
}
```


## Light sensor library
The light sensor library provides some basic functions for light sensor.

### Light Module

#### read()
+ **Description**
    Reads light data once from the sensor and stores it in the buffer.(the reading operation isblocking)
+ **Syntax**
    void read()
+ **Parameters**
    none
+ **Return**
    **int**: 0 if successes, nonzero value otherwise
+ **Usage**
    TL_Light.read()

#### data()
+ **Description**
    Reads light data from the buffer
+ **Syntax**
    double data()
+ **Parameters**
    none
+ **Return**
    **double**: light data stored in the buffer
+ **Usage**
    TL_Light.data()
+ **Example**
```c++
void setup() {
    TL_Serial.begin(9600);
}

void loop() {
    TL_Time.delayMillis(1000);
    TL_Light.read();
    TL_Serial.print("Light data is ");
    TL_Serial.println(TL_Light.data());    
}
```

