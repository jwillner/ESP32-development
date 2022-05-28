Start Here
-------------

Getting Started with PlatformIO. https://www.youtube.com/watch?v=JmvMvIphMnY.  

https://dronebotworkshop.com/platformio/.  
https://randomnerdtutorials.com/projects-esp32/.  


Debugging with ESP32-Prog 
--------
https://www.instructables.com/How-to-Use-a-Debugger-on-an-ESP32/.  

How to use the PlatformIO debugger on the ESP32 using an ESP-prog. https://www.youtube.com/watch?v=TivyIFF-dzw.      
Andreas Spiess #274 Free Inline Debugging for ESP32 and Arduino Sketches https://www.youtube.com/watch?v=psMqilqlrRQ




Hardware Guideline for ESP32

https://www.espressif.com/sites/default/files/documentation/esp32_hardware_design_guidelines_en.pdf

Hardware Guideline for ESP32-Wroom32

https://www.espressif.com/sites/default/files/documentation/esp32-wroom-32_datasheet_en.pdf

https://randomnerdtutorials.com/esp32-pinout-reference-gpios/

ESP32 deep sleep mode 

https://www.youtube.com/watch?v=y1R2y8dCsIg
https://www.youtube.com/watch?v=r75MrWIVIw4

ESP32 Excel Sheet from Andreas Spiess
https://github.com/SensorsIot/ESP32-Deep-Sleep/blob/master/ESP32.xlsx



# ESP32 Audio Tutorial with lots of examples
----------
https://www.youtube.com/watch?v=a936wNgtcRA

Links:
Phil's Library: https://github.com/pschatzmann/arduin...
Phil's A2DP library (Needed for Bluetooth): https://github.com/pschatzmann/ESP32-...
ESP32 board: https://s.click.aliexpress.com/e/_9fcxid
Microphone: https://s.click.aliexpress.com/e/_ABXMq1
MAX98357A I2S Amplifier: https://s.click.aliexpress.com/e/_A8FZaH
PCM5102 DAC: https://s.click.aliexpress.com/e/_AdOLAl
I2S ADC: https://s.click.aliexpress.com/e/_9zMQg5
ESP32 Audio Kit: https://s.click.aliexpress.com/e/_9QwJyD
PMOD "Soundcard": https://digilent.com/shop/pmod-i2s2-s...
Filter Video: https://youtu.be/D0EUDRo4Mx0
I2S Pins: https://bit.ly/3KAkkmv

#Getting started with Esp32 and PlatformIO | ESP-IDF | Visual Studio Code | ESP IDF C++ | Esp32 C++
https://www.youtube.com/watch?v=K-9oDE0-XsE

Links and references:-
•  ESP IDF GitHub repository:- https://github.com/espressif/esp-idf
•  ESP-IDF Programming Guide :- https://docs.espressif.com/projects/e...
•  Abiots GitHub link:- https://github.com/AbIots/AbiotsEsp32...
• ESP32 Template application:- https://github.com/AbIoTsolution/esp-...

We have a playlist dedicated entirely to ESP32:- https://youtube.com/playlist?list=PLa...
I hope you enjoy the video and please stay inside and stay safe!

# Program ESP32 devices using the ESP-IDF framework in Visual Studio Code or Eclipse
https://embeddedtutorials.com/eps32/get-started-with-esp-idf-windows/


Schweizer Cloud Infrastruktur - ProCloud AG, Schweiz
Infrastructure as a Service mit der Möglichkeit zusätzlicher managed Services.
procloud.ch/IAAS/Schweiz


IR Remote Control
-----

https://www.youtube.com/watch?v=8E3ltjnbV0c


0:11 / 6:05


# ESP32 Audio Output Using I2S and built-in Digital to Analogue Converters (DACs)
https://www.youtube.com/watch?v=lgDu88Y411o

atomic14

If you like ESP32 audio videos - I've got a complete set on this playlist: https://www.youtube.com/playlist?list...

GitHub links:
https://github.com/atomic14/esp32_aud...
and
https://github.com/atomic14/esp32_aud...


#252 ESP32 Ultra Low Power (ULP) core made easy in the Arduino IDE including 100$ challenge. 
https://www.youtube.com/watch?v=-QIcUTBB7Ww.  

# Installing SPI-FFS with Visual Code on ESP32
--------
inspired from: https://randomnerdtutorials.com/esp32-vs-code-platformio-spiffs/

Creating a data Folder
Create a folder called data inside your project folder. This can be done on VS Code.
With your mouse, select the project folder you’re working on. Click on the New Folder icon to create a new folder.
This new folder must be called data, otherwise, it won’t work.

Then, select the newly created data folder and create the files you want to upload by clicking on the New File icon. In this example, we’ll create a file called text.txt. You can create and upload any other file types like .html, .css or .js files, for example.

Uploading Filesystem Image
------
After creating and saving the file or files you want to upload under the data folder, follow the next steps:

Click the PIO icon at the left side bar. The project tasks should open.
Select env:esp32doit-devkit-v1 (it may be slightly different depending on the board you’re using).
Expand the Platform menu.
Select Build Filesystem Image.
Finally, click Upload Filesystem Image.

Testing
--------
Now, let’s just check if the file was actually saved into the ESP32 filesystem. Copy the following code to the main.cpp file and upload it to your board.

```
/*********
  Rui Santos
  Complete project details at https://RandomNerdTutorials.com/esp32-vs-code-platformio-spiffs/  
*********/

#include <Arduino.h>
#include "SPIFFS.h"
 
void setup() {
  Serial.begin(9600);
  if(!SPIFFS.begin(true)){
    Serial.println("An Error has occurred while mounting SPIFFS");
    return;
  }
  File file = SPIFFS.open("/text.txt");
  if(!file){
    Serial.println("Failed to open file for reading");
    return;
  }
  Serial.println("File Content:");
  while(file.available()){
    Serial.write(file.read());
  }
  file.close();
}
void loop() {
}
```
 
 
### ESP32 Webserver
-----------

inspired by https://randomnerdtutorials.com/esp32-web-server-arduino-ide/
```
/*********
  Rui Santos
  Complete project details at https://randomnerdtutorials.com  
*********/

// Load Wi-Fi library
#include <WiFi.h>

// Replace with your network credentials
const char* ssid = "REPLACE_WITH_YOUR_SSID";
const char* password = "REPLACE_WITH_YOUR_PASSWORD";

// Set web server port number to 80
WiFiServer server(80);

// Variable to store the HTTP request
String header;

// Auxiliar variables to store the current output state
String output26State = "off";
String output27State = "off";

// Assign output variables to GPIO pins
const int output26 = 26;
const int output27 = 27;

// Current time
unsigned long currentTime = millis();
// Previous time
unsigned long previousTime = 0; 
// Define timeout time in milliseconds (example: 2000ms = 2s)
const long timeoutTime = 2000;

void setup() {
  Serial.begin(115200);
  // Initialize the output variables as outputs
  pinMode(output26, OUTPUT);
  pinMode(output27, OUTPUT);
  // Set outputs to LOW
  digitalWrite(output26, LOW);
  digitalWrite(output27, LOW);

  // Connect to Wi-Fi network with SSID and password
  Serial.print("Connecting to ");
  Serial.println(ssid);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  // Print local IP address and start web server
  Serial.println("");
  Serial.println("WiFi connected.");
  Serial.println("IP address: ");
  Serial.println(WiFi.localIP());
  server.begin();
}

void loop(){
  WiFiClient client = server.available();   // Listen for incoming clients

  if (client) {                             // If a new client connects,
    currentTime = millis();
    previousTime = currentTime;
    Serial.println("New Client.");          // print a message out in the serial port
    String currentLine = "";                // make a String to hold incoming data from the client
    while (client.connected() && currentTime - previousTime <= timeoutTime) {  // loop while the client's connected
      currentTime = millis();
      if (client.available()) {             // if there's bytes to read from the client,
        char c = client.read();             // read a byte, then
        Serial.write(c);                    // print it out the serial monitor
        header += c;
        if (c == '\n') {                    // if the byte is a newline character
          // if the current line is blank, you got two newline characters in a row.
          // that's the end of the client HTTP request, so send a response:
          if (currentLine.length() == 0) {
            // HTTP headers always start with a response code (e.g. HTTP/1.1 200 OK)
            // and a content-type so the client knows what's coming, then a blank line:
            client.println("HTTP/1.1 200 OK");
            client.println("Content-type:text/html");
            client.println("Connection: close");
            client.println();
            
            // turns the GPIOs on and off
            if (header.indexOf("GET /26/on") >= 0) {
              Serial.println("GPIO 26 on");
              output26State = "on";
              digitalWrite(output26, HIGH);
            } else if (header.indexOf("GET /26/off") >= 0) {
              Serial.println("GPIO 26 off");
              output26State = "off";
              digitalWrite(output26, LOW);
            } else if (header.indexOf("GET /27/on") >= 0) {
              Serial.println("GPIO 27 on");
              output27State = "on";
              digitalWrite(output27, HIGH);
            } else if (header.indexOf("GET /27/off") >= 0) {
              Serial.println("GPIO 27 off");
              output27State = "off";
              digitalWrite(output27, LOW);
            }
            
            // Display the HTML web page
            client.println("<!DOCTYPE html><html>");
            client.println("<head><meta name=\"viewport\" content=\"width=device-width, initial-scale=1\">");
            client.println("<link rel=\"icon\" href=\"data:,\">");
            // CSS to style the on/off buttons 
            // Feel free to change the background-color and font-size attributes to fit your preferences
            client.println("<style>html { font-family: Helvetica; display: inline-block; margin: 0px auto; text-align: center;}");
            client.println(".button { background-color: #4CAF50; border: none; color: white; padding: 16px 40px;");
            client.println("text-decoration: none; font-size: 30px; margin: 2px; cursor: pointer;}");
            client.println(".button2 {background-color: #555555;}</style></head>");
            
            // Web Page Heading
            client.println("<body><h1>ESP32 Web Server</h1>");
            
            // Display current state, and ON/OFF buttons for GPIO 26  
            client.println("<p>GPIO 26 - State " + output26State + "</p>");
            // If the output26State is off, it displays the ON button       
            if (output26State=="off") {
              client.println("<p><a href=\"/26/on\"><button class=\"button\">ON</button></a></p>");
            } else {
              client.println("<p><a href=\"/26/off\"><button class=\"button button2\">OFF</button></a></p>");
            } 
               
            // Display current state, and ON/OFF buttons for GPIO 27  
            client.println("<p>GPIO 27 - State " + output27State + "</p>");
            // If the output27State is off, it displays the ON button       
            if (output27State=="off") {
              client.println("<p><a href=\"/27/on\"><button class=\"button\">ON</button></a></p>");
            } else {
              client.println("<p><a href=\"/27/off\"><button class=\"button button2\">OFF</button></a></p>");
            }
            client.println("</body></html>");
            
            // The HTTP response ends with another blank line
            client.println();
            // Break out of the while loop
            break;
          } else { // if you got a newline, then clear currentLine
            currentLine = "";
          }
        } else if (c != '\r') {  // if you got anything else but a carriage return character,
          currentLine += c;      // add it to the end of the currentLine
        }
      }
    }
    // Clear the header variable
    header = "";
    // Close the connection
    client.stop();
    Serial.println("Client disconnected.");
    Serial.println("");
  }
}
```



