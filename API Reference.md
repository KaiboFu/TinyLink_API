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
+ **Descriptio**  
    Before using serial, the data rate in bits per second (baud) must be set for transmission. For communicating with the computer, use one of these rates: 300, 600, 1200, 2400, 4800, 9600, 14400, 19200, 28800, 38400, 57600, or 115200. You can, however, specify other rates. For communication between two devices, the data rate must be set at the same value.
+ **Synta**    
    void begin(unsigned long speed)
+ **Parameters**  
    **speed**: in bits per second (baud)
+ **Retur**    
    none
+ **Usag**    
    TL_Serial.begin(speed)
+ **Exampl**    
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
+ **Descriptio**  
    Disables serial communication, allowing the RX and TX pins to be used for general input and output. To re-enable serial communication, call TL_Serial.begin().
+ **Synta**  
    void end()
+ **Parameters**
    none
+ **Retur**  
    none
+ **Usag**  
    TL_Serial.end()
+ **Exampl**  
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
+ **Descriptio**  
    Gets the number of bytes (characters) available for reading from the serial port. This is data that's already arrived and stored in the serial receive buffer(which holds 64 bytes just for Arduino UNO). 
+ **Synta**  
    int available()
+ **Parameters**
    none
+ **Retur**  
    **int**: the number of bytes available to read; if there is nothing available the returning     number is 0; if there is something wrong with the serial the returning number is negative
+ **Usag**  
    TL_Serial.available()
+ **Exampl**  
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
+ **Descriptio**  
    Reads the first byte of incoming serial data.
+ **Synta**  
   int read()
+ **Parameters**
    none
+ **Retur**  
    **int**: the first byte of incoming serial data available (or -1 if no data is available)
+ **Usag**  
    TL_Serial.read()
+ **Exampl**  
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
+ **Descriptio**  
    Prints data to the serial port as human-readable ASCII text. This command can take many forms. Numbers are printed using an ASCII character for each digit. Floats are similarly printed as ASCII digits, defaulting to two decimal places. Bytes are sent as a single character. Characters and strings are sent as is, e.g., TL_Serial.print(78) gives "78", TL_Serial.print(78.123) gives "78.12",  TL_Serial.print('a') gives "a" and TL_Serial.print('abc') gives "abc"
+ **Synta**  
    int print(char val)
    int print(int val)
    int print(long val)
    int print(double val)
    int print(const char* val)
    int print(const String &val)
+ **Parameters**
    **val**: the value to print
+ **Retur**  
    **int**: the number of bytes written, though reading that number is optional
+ **Usag**  
    TL_Serial.print(val)
+ **Exampl**  
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
+ **Descriptio**  
    Prints data to the serial port as human-readable ASCII text followed by a carriage return character (ASCII 13, or '\r') and a newline character (ASCII 10, or '\n'). This command takesthe same forms as TL_Serial.print().
+ **Synta**  
    int println(char val)
    int println(int val)
    int println(long val)
    int println(double val)
    int println(const char* val)
    int println(const String &val)
+ **Parameters**
    **val**: the value to print 
+ **Retur**  
    **int**: the number of bytes written, though reading that number is optional
+ **Usag**  
    TL_Serial.println(val)
+ **Exampl**  
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
+ **Descriptio**  
    Returns the number of milliseconds since the board began running the current program. This number will go back to zero after overflow occurs.
+ **Synta**  
    unsigned long millsFromStart()
+ **Parameters**
    none
+ **Retur**  
    **unsigned long**: Number of milliseconds since the program started
+ **Usag**  
    TL_Time.millisFromStart()  
+ **Exampl**  
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
+ **Descriptio**  
    Returns the number of microseconds since the board began running the current program. This number will go back to zero after overflow occurs.(There are 1,000 microseconds in a millisecond and 1,000,000 microseconds in a second)
+ **Synta**  
    unsigned long microsFromStart()
+ **Parameters**
    none
+ **Retur**  
    **unsigned long**: Number of microseconds since the program started
+ **Usag**  
    TL_Time.microsFromStart()
+ **Exampl**  
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
+ **Descriptio**  
    Pauses the program for the amount of time (in milliseconds) specified as parameter. (There are 1000 milliseconds in a second.)
+ **Synta**  
    void delayMillis(unsigned long ms)
+ **Parameters**
    none
+ **Retur**  
    **ms**: the number of milliseconds to pause
+ **Usag**  
    TL_Time.delayMillis(ms)
+ **Exampl**  
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
+ **Descriptio**  
    Pauses the program for the amount of time (in microseconds) specified as parameter. There are a thousand microseconds in a millisecond, and a million microseconds in a second.
+ **Synta**  
    void delayMicros(unsigned long us)
+ **Parameters**
    none
+ **Retur**  
    **us**: the number of microseconds to pause
+ **Usag**  
    TL_Time.delayMicrosus)
+ **Exampl**  
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
+ **Descriptio**  
    Before using a timer, the timer must be started. A timer can only be started once(unless you have stopped it)
+ **Synta**  
   bool start()
+ **Parameters**
    none
+ **Retur**  
    **bool**: true on success; false on failure
+ **Usag**  
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
+ **Descriptio**  
    Stops the timer(if you want to reuse the timer, you must start the timer again)
+ **Synta**  
   bool stop()
+ **Parameters**
    none
+ **Retur**  
    **bool**: true on success; false on failure
+ **Usag**  
  TL_Timer.stop()
  ***or***
  TL_Timer1.stop()
  ***or***
  TL_Timer2.stop()
  ………
  ***or***
  TL_Timern.stop()
+ **Exampl**  
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
+ **Descriptio**  
    Attaches the callback function to a Timer object. When the timer expires, the callback function will be executed.
+ **Synta**  
    void attachInterrupt(void (* callback) ())
+ **Parameters**
    **callback**: the callback function for a Timer object,
+ **Retur**  
    none
+ **Usag**  
    TL_Timer.attachInterrupt(callback)
    ***or***
    TL_Timer1.attachInterrupt(callback)
    ***or***
    TL_Timer2.attachInterrupt(callback)
    ………
    ***or***
    TL_Timern.attachInterrupt(callback)
    (Note: n is a numberic that is less than 8 and we provide 8 software timers for users. The users need to write the callback function by themselves )
+ **Exampl**  
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
+ **Descriptio**  
    Detaches the callback function from a Timer object
+ **Synta**  
    void detachInterrupt()
+ **Parameters**
    none
+ **Retur**  
    none
+ **Usag**  
    TL_Timer.detachInterrupt()
    ***or***
    TL_Timer1.detachInterrupt()
    ***or***
    TL_Timer2.detachInterrupt()
    ………
    ***or***
    TL_Timern.detachInterrupt()
    (Note: n is a numberic that is less than 8 and we provide 8 software timers for users )
+ **Exampl**  
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
+ **Descriptio**  
    Sets the period(in milliseconds) and the type of a Timer object, e.g. TIMER_ONE_SHOT(expiring just once), TIMER_PERIODIC(repeatedly expiring after the initial expiration). A timer can be set more than once.
+ **Synta**  
    void setPeriod(unsigned long ms, int type = TIMER_PERIODIC)
+ **Parameters**
    **ms**: the period in millisecond of the timer
    **typ**  : the type of the timer, which can only be TIMER_ONE_SHOT(0) or TIEMR_PERIODIC(1)   and the type defaults to TIMER_PERIODIC
+ **Retur**  
    none
+ **Usag**  
    TL_Timer.setPeriod(ms, type)
    ***or***
    TL_Timer1.setPeriod(ms, type)
    ***or***
    TL_Timer2.setPeriod(ms, type)
    ………
    ***or***
    TL_Timern.setPeriod(ms, type)
    (Note: n is a numberic that is less than 8 and we provide 8 software timers for users )
+ **Exampl**  
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
+ **Descriptio**  
    Sets the frequency (in Hz) and the type of a Timer, e.g. TIMER_ONE_SHOT(expiring just once), TIMER_PERIODIC(repeatedly expiring after the initial expiration). A timer can be set more than once.
+ **Synta**  
    void setFrequency(unsigned long freq, int type = TIMER_PERIODIC)
+ **Parameters**
    **freq**: the frequency of the timer
    **typ**  : the type of the timer, which can only be TIMER_ONE_SHOT(0)or TIEMR_PERIODIC(1)     and the type defaults to TIMER_PERIODIC
+ **Retur**  
    none
+ **Usag**  
    TL_Timer.setFrequency(frep, type)
    ***or***
    TL_Timer1.setFrequency(frep, type)
    ***or***
    TL_Timer2.setFrequency(frep, type)
    ………
    ***or***
    TL_Timern.setFrequency(frep, type)
    (Note: n is a numberic that is less than 8 and we provide 8 software timers for users)
+ **Exampl**  
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
+ **Descriptio**  
    Initializes the storage module. The initialization is necessasy before using the stroage module
+ **Synta**  
    bool begin()
+ **Parameters**
    none
+ **Retur**  
    **bool**: true on success; false on failure 
+ **Usag**  
    TL_Storage.begin()

#### open()
+ **Descriptio**  
    Opens a file in the storage
+ **Synta**  
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

+ **Retur**  
    **TL_Fil**  : a File object referring to the opened file; if the file couldn't be opened, this object will evaluate to false in a boolean context, i.e. you can test the return value with "if (f)". More details about the File type, please refer to the next File Module
+ **Usag**  
    TL_Storage.open(filepath)
    ***or***
    TL_Storage.open(filepath, mode)
+ **Exampl**  
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
+ **Descriptio**  
    Checks whether a file or directory exists in the storage module. 
+ **Synta**  
    bool exists(cosnt char *filepath)   
    bool exists(const String &filepath)
+ **Parameters**
    **filepath**: the name the file/directory to check for existence and the file path is a relative path, e.g exist(“a.txt”), exist(“1/2/3”)
+ **Retur**  
    **bool**: true means existing; false means not existing
+ **Usag**  
    TL_Storage.exists(filepath)
+ **Exampl**  
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
+ **Descriptio**  
    Creates a directory in the storage module. This will also create any intermediate directories that don't already exists; e.g. TL_Storage.mkdir("a/b/c") will create a, b, and c
+ **Synta**  
    bool mkdir(const char *filepath)
    bool mkdir(cosnt string &filepath)
+ **Parameters**
    **filepath**: the name of the directory to create, with sub-directories separated by forward-slashes, “/”. The filepath is a relative file path.
+ **Retur**  
    **bool**: true if the creation of the directory succeeded, false if not
+ **Usag**  
    TL_Storage.mkdir(filepath)
+ **Exampl**  
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
+ **Descriptio**  
    Removes a file from the external storage.
+ **Synta**  
    bool remove(const char *filename)
    bool remove(const String &filename)
+ **Parameters**
    **filenam**  : the name of the file to remove, with sub-directories separated by forward- slashes, "/".The filepath is a relative file path.
+ **Retur**  
    **bool**: true on success; false on failure
+ **Usag**  
    TL_Storage.remove(filepath)
+ **Exampl**  
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
+ **Descriptio**  
    Removes a directory from the external storage. The directory must be empty
+ **Synta**  
    bool remove(cosnt char *filepath)
    bool remove(const String &filepath)
+ **Parameters**
    **filepath**: the name of the directory to remove, with sub-directories separated by forward-slashes, /The filepath is a relative file path.
+ **Retur**  
    **bool**: true on success; false on failure
+ **Usag**  
    TL_Storage.rmdir(filepath)
+ **Exampl**  
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
+ **Descriptio**  
    Closes the file, and ensure that any data written to it is physically saved to the storage.
+ **Synta**  
    bool close()
+ **Parameters**
    none
+ **Retur**  
    **int**: true on success; false on failure
+ **Usag**  
    TL_File fp = TL_Storage.open(filepath, mode);
    …..
    fp.close(); 
    (Note: TL_File is a artificial Module and you can declare and define objects of TL_File type)
+ **Exampl**  
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
+ **Descriptio**  
    Reads one byte from the file return it or reads some bytes from the file and stores them in the buffer
+ **Synta**  
    int read()
    int read(char* buf, int size)
+ **Parameters**
    **buf**: an array of characters or bytes where the reading bytes are stored
    **siz**  : the number of bytes read from the file
+ **Retur**  
    **int**: for call with no parameters, the return value is the obtained byte and for call with two parameters, the return value the number of bytes read, which may be less than size if an error or end-of-file condition occurs
+ **Usag**  
    TL_File fp = TL_Storage.open(filepath, mode);
    …… 
    int ch = fp.read();
    ***or*** 
    TL_File fp = TL_Storage.open(filepath, mode);
    ……
    int ch = fp.read(buf, size);
    (Note: TL_File is a artificial Module and you can declare and define objects of TL_File type)
+ **Exampl**  
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
+ **Descriptio**  
    writes data to the file; returns the number of bytes written
+ **Synta**  
    int write(const char data)
    int write(const char* buf)
    int write(const String& buf)
+ **Parameters**
    **data**: the char to write
    **buf**: an array of characters or bytes
+ **Retur**  
    **int**: the number of bytes written, though reading that number is optional
+ **Usag**  
    TL_File fp = TL_Storage.open(filepath, mode);
    …… 
    fp.write(data);
    ***or***
    TL_File fp = TL_Storage.open(filepath, mode);
    …… 
    fp.write(data, size);
    (Note: TL_File is a artificial Module and you can declare and define objects of TL_File type)
+ **Exampl**  
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
+ **Descriptio**  
    Ensures that any bytes written to the file are physically saved to the  storage area. This is done automatically when the file is closed.
+ **Synta**  
    void flush()
+ **Parameters**
    none
+ **Retur**  
    none
+ **Usag**  
    TL_File fp = TL_Storage.open(filepath, mode);
    …… 
    fp.write(data);
    fp.flush();
    (Note: TL_File is a artificial Module and you can declare and define objects of TL_File type)
+ **Exampl**  
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
+ **Descriptio**  
    Gets the current position of the file pointer
+ **Synta**  
    unsigned long position()
+ **Parameters**
    none
+ **Retur**  
    **long**: the position of the file pointer
+ **Usag**  
    TL_File fp = TL_Storage.open(filepath, mode);
    …..
    long pos = fp.position(); 
    (Note: TL_File is a artificial Module and you can declare and define objects of TL_File type)
+ **Exampl**  
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
+ **Descriptio**  
    Shifts the file pointer for a offset distance relative to the beginning of the file
+ **Synta**  
    int seek(long offset)
+ **Parameters**
    **offset**: number of characters to shift the file pointer relative to the beginning of the file
+ **Retur**  
    **int**: 0 on success, nonzero value otherwise
+ **Usag**  
    TL_File fp = TL_Storage.open(filepath, mode);
    …..
    fp.seek(offset); 
    (Note: TL_File is a artificial Module and you can declare and define objects of TL_File type)
+ **Exampl**  
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
+ **Descriptio**  
    Gets the size of the file
+ **Synta**  
    unsigned long size()
+ **Parameters**
    none
+ **Retur**  
    **unsigned long**: the size of the file in bytes
+ **Usag**  
    TL_File fp = TL_Storage.open(filepath, mode);
    …..
    unsigned longf_size = fp.size(); 
    (Note: TL_File is a artificial Module and you can declare and define objects of TL_File type)

# Extended API

## TL_WiFi library
The TL_WiFi library allows for initializing the WiFi hardare and network setting.
### WiFi Module

#### init()
+ **Descriptio**  
    Initializes the WiFi hardware module. Initialization is necassary before using Wifi module
+ **Synta**  
    bool init()
+ **Parameters**
    none
+ **Retur**  
    **bool**: true on success; false on failure
+ **Usag**  
    TL_WiFi.init()

#### join()
+ **Descriptio**  
    Connects to the router named with the SSID; Return true on success or false on failure
+ **Synta**  
    void join(cosnt char \*SSID, const char \*PassW = "")
    void join(cosnt String &SSID, const String &PassW = "")
+ **Parameters**
    **SSID**: the SSID of the router  
    **PassW**: the password of the router
+ **Retur**  
    **bool**: true on success; false on failure
+ **Usag**  
    TL_WiFi.join(SSID)
    ***or****
    TL_WiFi.join(SSID, PassW)
+ **Exampl**  
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
+ **Descriptio**  
    Disconnects from the router; Return true on success or false on failure
+ **Synta**  
    bool disjoin()
+ **Parameters**
    none
+ **Retur**  
    **bool**: true on success; false on failure
+ **Usag**  
    TL_WIFI.disjoin(SSID)
+ **Exampl**  
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
+ **Descriptio**  
    Fetch a HTTP client from the WiFi module that can send and receive data through HTTP protocol.
+ **Synta**  
    TL_HTTP fetchHTTP()
+ **Parameters**
    none
+ **Retur**  
    **TL_HTTP**: a HTTP client object built from the WiFi network. More details about the TL_HTTP type, please refer to the TL_HTTP library.
+ **Usag**  
    TL_WiFi.fetchHTTP()
+ **Exampl**  
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
+ **Descriptio**  
    Fetch a MQTT client from the WiFi module that can subscirbe and publish topics through MQTT protocol.
+ **Synta**  
    TL_MQTT fetchMQTT()
+ **Parameters**
    none
+ **Retur**  
    **TL_MQTT**: a MQTT client object built from the WiFi network. More details about the TL_MQTT type, please refer to the TL_MQTT library.
+ **Usag**  
    TL_WiFi.fetchMQTT()
+ **Exampl**  
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
+ **Descriptio**  
    Request data from a specified resource(e.g., URL) via HTTP method
+ **Synta**  
    bool get(const char\* url)
    bool get(const String& url)
+ **Parameters**
    **url**: the URL of resource, e.g., "http://host[:port]/path"
+ **Retur**  
    **bool**: true on success; false on failure
+ **Usag**  
    TL_HTTP http_client = TL_WiFi.fetchHTTP()
    ...
    http_client.get(url)
+ **Exampl**  
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
+ **Descriptio**  
    Submits data to be processed to a specified resource (e.g., URL) via HTTP POST method
+ **Synta**  
    bool post(const String &url, const String &data)
    bool post(const char\* url, const char\* data)
+ **Parameters**
    **url**: the URL of the resource
    **data**: the content to post to the remote host and the format of data must be of the specific format, e.g. name=xxx&age=xxx
+ **Retur**  
    **bool**: true on success; false on failure
+ **Usag**  
    TL_HTTP http_client = TL_WiFi.fetchHTTP()
    ...
    http_client.post(url, data)
+ **Exampl**  
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
+ **Descriptio**  
    Get the data returned form the HTTP Post or Get request.
+ **Synta**  
    const String& getResponse()
+ **Parameters**
    none
+ **Retur**  
    **const String&**: the response string get from the Post/Get request
+ **Usag**  
    TL_HTTP http_client = TL_WiFi.fetchHTTP()
    ...
    http_client.post(url, data)
    String res = http_client.getResponse()
    ***or***
    TL_HTTP http_client = TL_WiFi.fetchHTTP()
    ...
    http_client.get(url)
    String res = http_client.getResponse()
+ **Exampl**  
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
+ **Descriptio**  
    Connecs to a remote server with specified options(Sends an MQTT connection packet). After execution, all connection options are stored internally for 
+ **Synta**  
    int connect(const String& serverName, int port, const String& clientName, const String& userName= "", const String& passW = "")
    int connect(const char\* serverName, int port, const char\* clientName, const char\* userName= "", const char\* passW= "")
+ **Parameters**
    **severNam**  : the hostname of the remote server
    **port**: the port number
    **clientNam**  : the clientID
    **userNam**  ：the username
    **passW**: the password of the user
+ **Retur**  
    **int**: 0 if successes, nonzero value otherwise
+ **Usag**  
    TL_MQTT mqtt_client = TL_WiFi.fetchMQTT()
    ...
    mqtt_client.connect(serverName, port, clientName)
    ***or***
    TL_MQTT mqtt_client = TL_WiFi.fetchMQTT()
    ...
    mqtt_client.connect(serverName, port, clientName, userName, passW)
+ **Exampl**  

#### reconnect()
+ **Descriptio**  
    Reconnects to the remote server with previously stored connection options(Sends an MQTT connection packet again)
+ **Synta**  
    int reconnect()
+ **Parameters**
    none
+ **Retur**  
    **int**: 0 if successes, nonzero value otherwise
+ **Usag**  
    TL_MQTT mqtt_client = TL_WiFi.fetchMQTT()
    ...
    mqtt_client.connect(serverName, port, clientName)
    ...
    mqtt_client.reconnnect()
+ **Exampl**  

#### disconnect()
+ **Descriptio**  
    Disconnect to the remote server that the client previously connected to and clear up all state(Sends an MQTT disconnection packet)
+ **Synta**  
    int disconnect()
+ **Parameters**
    none
+ **Retur**  
    **int**: 0 if successes, nonzero value otherwise
+ **Usag**  
    TL_MQTT mqtt_client = TL_WiFi.fetchMQTT()
    ...
    mqtt_client.connect(serverName, port, clientName)
    ...
    mqtt_client.disconnnect()
+ **Exampl**  

#### isConnected()
+ **Descriptio**  
    Check whether the client and server are still connectiong to each other
+ **Synta**  
    bool isConnected()
+ **Parameters**
    none
+ **Retur**  
    **bool**: ture if connected, false otherwise
+ **Usag**  
    TL_MQTT mqtt_client = TL_WiFi.fetchMQTT()
    ...
    mqtt_client.connect(serverName, port, clientName)
    ...
    if(mqtt_client.isConnected()) {
        ...
    }
+ **Exampl**  

#### publish()
+ **Descriptio**  
    Sends a message to the client/server(Sends an MQTT publish packet)

+ **Synta**  
    int publish(const String& topicName, const String& data, int length, int qos = 0<!---, bool retained = false-->)
    int publish(const char\* topicName, const char\* data, int length, int qos = 0<!---, bool retained = false-->)

    <!-- int publish(const char\* topicName, const char\* data, unsigned short& id, int qos = 1, bool retained = false) int publish(const String& topicName, const String& data, unsigned short& id, int qos = 1) -->

+ **Parameters**
    **topicNam**  : the topic to be published
    **data**: the concrete content of the sent message
    **length**: the length of sent message
    **qos**: the QoS to send the data at. Valid value is 0,1,2(Larger value means better quality of service).
    <!---**id**: the packet id--><!---**retianed**: whether the message should be retained-->
+ **Retur**  
    **int**: 0 if successes, nonzero value otherwise

+ **Usag**  
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

+ **Exampl**  
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
+ **Descriptio**  
    Subscribe a topic(Sends an MQTT subscribe packet)
+ **Synta**  
    int subscribe(const String& topicName, void (\*callback)(MessageData& md), int qos = 0)
    int subscribe(const char\* topicName, void (\*callback)(MessageData& md), int qos = 0)
+ **Parameters**
    **topicNam**  : the topic to be subscribed
    **callback**: the callback function to be invoked when a message is received for this subscription
    ***Not**  *: **MessageData** is actually a structure in Paho project, an open-source client implemetation of MQTT and MQTT-SN messaging protocols. More details, please refer to [MQTTCLient.h](https://github.com/eclipse/paho.mqtt.embedded-c/blob/master/MQTTClient/src/MQTTClient.h)
    **qos**: the QoS to subscribe at. Valid value is 0,1,2(Larger value means better quality of service).
+ **Retur**  
    **int**: 0 if successes, nonzero value otherwise
+ **Usag**  
    TL_MQTT mqtt_client = TL_WiFi.fetchMQTT();
    ...
    mqtt_client.connect(serverName, port, clientName);
    ...
    mqtt_client.subscribe(topicFilter, callback, qos);
+ **Exampl**  
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
+ **Descriptio**  
    Unsubscribe a topic(Sends an MQTT unsubscribe packet)
+ **Synta**  
    int unsubscribe(const String& topicName)
    int unsubscribe(const char* topicName)
+ **Parameters**
    **topicNam**  : the topic to be unsubscribed
+ **Retur**  
    **int**: 0 if successes, nonzero value otherwise
+ **Usag**  
    TL_MQTT mqtt_client = TL_WiFi.fetchMQTT()
    ...
    mqtt_client.connect(serverName, port, clientName)
    ...
    mqtt_client.unsubscribe(topicFilter)
+ **Exampl**  
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
+ **Descriptio**  
    Turns on the led
+ **Synta**  
    void turnOn()
+ **Parameters**
    none
+ **Retur**  
    none
+ **Usag**  
    TL_LED.turnOn()

#### turnOff()
+ **Descriptio**  
    Turns off the led
+ **Synta**  
    void turnOff()
+ **Parameters**
    none
+ **Retur**  
    none
+ **Usag**  
    TL_LED.turnOff()
+ **Exampl**  
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
+ **Descriptio**  
    Toggles the state of the led. If the led is on, turn off it and if the led is off, turn on the led
+ **Synta**  
    void toggle()
+ **Parameters**
    none
+ **Retur**  
    none
+ **Usag**  
    TL_LED.toggle
+ **Exampl**  
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
+ **Descriptio**  
    Reads PM25 data once from the sensor and stores it in the buffer.(the reading operation isblocking)
+ **Synta**  
    void read()
+ **Parameters**
    none
+ **Retur**  
    **int**: 0 if successes, nonzero value otherwise
+ **Usag**  
    TL_PM25.read()

#### data()
+ **Descriptio**  
    Reads PM25 data from the buffer
+ **Synta**  
    double data()
+ **Parameters**
    none
+ **Retur**  
    **doubl**  : PM25 data stored in the buffer
+ **Usag**  
    TL_PM25.data()
+ **Exampl**  
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
+ **Descriptio**  
    Reads humidity data once from the sensor and stores it in the buffer.(the reading operation isblocking)
+ **Synta**  
    void read()
+ **Parameters**
    none
+ **Retur**  
    **int**: 0 if successes, nonzero value otherwise
+ **Usag**  
    TL_Humidity.read()

#### data()
+ **Descriptio**  
    Reads humidity data from the buffer
+ **Synta**  
    double data()
+ **Parameters**
    none
+ **Retur**  
    **doubl**  : humidity data stored in the buffer
+ **Usag**  
    TL_Humidity.data()
+ **Exampl**  
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
+ **Descriptio**  
    Reads temperature data once from the sensor and stores it in the buffer.(the reading operation isblocking)
+ **Synta**  
    void read()
+ **Parameters**
    none
+ **Retur**  
    **int**: 0 if successes, nonzero value otherwise
+ **Usag**  
    TL_Temperature.read()

#### data()
+ **Descriptio**  
    Reads temperature data from the buffer
+ **Synta**  
    double data()
+ **Parameters**
    none
+ **Retur**  
    **doubl**  : temperature data stored in the buffer
+ **Usag**  
    TL_Temperature.data()
+ **Exampl**  
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
+ **Descriptio**  
    Reads soil humidity data once from the sensor and stores it in the buffer.(the reading operation isblocking)
+ **Synta**  
    void read()
+ **Parameters**
    none
+ **Retur**  
    **int**: 0 if successes, nonzero value otherwise
+ **Usag**  
    TL_Soil_Humidity.read()

#### data()
+ **Descriptio**  
    Reads soil humidity data from the __buffer__
+ **Synta**  
    double data()
+ **Parameters**
    none
+ **Retur**  
    **doubl**  : soil humidity data stored in the buffer
+ **Usag**  
    TL_Soil_Humidity.data()
+ **Exampl**  
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
+ **Descriptio**  
    Reads light data once from the sensor and stores it in the buffer.(the reading operation isblocking)
+ **Synta**  
    void read()
+ **Parameters**
    none
+ **Retur**  
    **int**: 0 if successes, nonzero value otherwise
+ **Usag**  
    TL_Light.read()

#### data()
+ **Descriptio**  
    Reads light data from the buffer
+ **Synta**  
    double data()
+ **Parameters**
    none
+ **Retur**  
    **doubl**  : light data stored in the buffer
+ **Usag**  
    TL_Light.data()
+ **Exampl**  
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

