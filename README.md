# Internet of Things First Task

In this task we using [Wokwi](https://wokwi.com) and select ESP32 then we connect it with 4 LED 

![image](https://github.com/amf17/IOT_Task1/assets/139582388/1232c4e5-8407-46a7-92ce-c02399148a49)


## Introduction:

The provided code implements a remote control robot system using an ESP32 microcontroller, WiFi connectivity, and HTTP communication. The system connects to a specified WiFi network, establishes an HTTP connection to a remote server, and retrieves commands to control the car's movement. The received commands determine the robot's direction—forward, backward, left, or right. The code uses the "WiFi.h" and "HTTPClient.h" libraries for WiFi communication and HTTP requests, respectively.

## Hardware Setup:

1- ESP32 Microcontroller: The heart of the system, responsible for connecting to the WiFi network and executing the control logic.

2- Motors: The car's movement is controlled by four motors, connected to GPIO pins 25, 26, 27, and 33 on the ESP32.

3- WiFi Network: The ESP32 connects to a WiFi network with the SSID "Wokwi-GUEST" (you can replace this with your desired network).

4- Remote Server: The system communicates with a remote server using HTTP requests to receive control commands.

## Code Explanation:
```
#include <WiFi.h> 
#include <HTTPClient.h>

const char* ssid = "Wokwi-GUEST"; 
const char* password = "";

const String url = "https://s-m.com.sa/b.html"; 
String payload = ""; 
void setup() {
   Serial.begin(115200); 
   WiFi.begin(ssid, password); 
   pinMode(27, OUTPUT); 
   pinMode(33, OUTPUT);
   pinMode(25, OUTPUT);
   pinMode(26, OUTPUT); 

  
   Serial.print("Connecting to WiFi"); 
   while (WiFi.status() != WL_CONNECTED) {
     delay(500); 
     Serial.print("."); 
  }

Serial.print("OK! IP="); 
Serial.println(WiFi.localIP());

Serial.print("Fetching " + url + "... ");




}

void loop() { 
  HTTPClient http; 
  http.begin(url); int 
  httpResponseCode = http.GET(); 
  if (httpResponseCode > 0) { 
    Serial.print("HTTP "); 
    Serial.println(httpResponseCode); 
    payload = http.getString(); 
    Serial.println(); 
    Serial.println(payload); 
    if( payload == "forward" ){ 
      digitalWrite(25, HIGH);
    }else { 
      digitalWrite(25, LOW);} 
      if( payload == "backward" ){ 
      digitalWrite(26, HIGH); 
    }else{ 
      digitalWrite(26, LOW);} 
      if( payload == "right" ){ 
      digitalWrite(27, HIGH); 
    }else{ 
      digitalWrite(27, LOW);} 
      if( payload == "left" ){ 
      digitalWrite(33, HIGH); 
    }else{ 
      digitalWrite(33, LOW); 
    } 
    }else{ 
    Serial.print("Error code: ");
    Serial.println(httpResponseCode); 
    Serial.println(":-("); 
  }

}
```
1- Importing Libraries: The code starts by importing the necessary libraries for WiFi and HTTP communication.

2- WiFi Configuration: The code defines the WiFi SSID and password for the network it will connect to.

3- URL Definition: The four URLs are:

https://s-m.com.sa/f.html: Represents the movement "forward."

https://s-m.com.sa/r.html: Represents the movement "right."

https://s-m.com.sa/l.html: Represents the movement "left."

https://s-m.com.sa/b.html: Represents the movement "backward.".


4- Setup Function: The setup() function initializes the serial communication for debugging and sets up the GPIO pins for controlling the robot.

5- WiFi Connection: The code attempts to connect to the specified WiFi network, displaying a loading animation until a connection is established.

6- HTTP Request: An HTTP GET request is made to the specified URL using the HTTPClient library. The response code is checked to ensure a successful connection.

7- Command Parsing: If the HTTP request is successful, the received payload is analyzed. Depending on the received command ("forward," "backward," "left," "right"), the corresponding GPIO pin is set to either HIGH or LOW, controlling the robot's direction.

8- Error Handling: If there's an error in the HTTP request, the error code is printed to the serial monitor.

### Forward 

![image](https://github.com/amf17/IOT_Task1/assets/139582388/51f4f620-6ad8-4222-ba40-82fde820c847)

### Backward 

![image](https://github.com/amf17/IOT_Task1/assets/139582388/88c11ef8-5064-4886-b350-0024f3ac2943)

### Right

![image](https://github.com/amf17/IOT_Task1/assets/139582388/bf451747-0080-4355-972e-0c4ddc3d5ad8)


### Left

![image](https://github.com/amf17/IOT_Task1/assets/139582388/17a3e878-3992-4e93-a539-6a5fc7a493c9)

## Conclusion:

The provided code demonstrates how an ESP32 microcontroller can be used to create a remote control robot system using WiFi and HTTP communication. It connects to a specified WiFi network, communicates with a remote server to receive control commands, and controls the robot's movement based on the received instructions. This project serves as a foundation for building more complex remote control systems and could be extended to include additional features such as camera streaming or obstacle detection.


