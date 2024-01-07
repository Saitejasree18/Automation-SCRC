# Automation-SCRC

**DESIGN APPROACH**

The basic automation structure includes three major components. They are IoT Devices, IoT gateway or control hub and output. Based on the type of gateway used ,this is classified into two types
  1)wired 
  2) wireless
In wired gateway we use ethernet as communication technology. The home equipment was installed with sensors and actuators in it and connected to the microcontroller(PLC) which is connected to the computer through ethernet cable.
In wireless communication technology there are various approaches such as
  1) RF transmitter and receiver:
Used for light loads. Input is given through a touch screen
  2) Global system for mobile communication:
The RF transmitter and receiver circuit is replaced by GSM module (SIM900) and connected to Arduino which is connected to Relay driver(ULN2003) and finally to the load.
The input is given as SMS of AT command or that starts with "#A. " and ends with "*" with command in between which is processed and given as input signal to the Arduino through GSM module.
  3) IR remote controlled communication:
The input is given through a IR remote which has predefined hex code for each button. If the hex code of input matches with the predefined then the button will operate. The IR signal from the remote is received with IR receiver (TSOP1738) and gives the signal to the Arduino which is connected to the load through relay drives and relays.
  4)via Bluetooth:
An Android app in the mobile connects the Bluetooth to the module (HC-05). This Bluetooth maintains the entire connectivity of the system to the mobile and acts as the communication medium. The Bluetooth module is connected to Arduino and then to load through relay.
But the Bluetooth can maintain the connectivity only upto a certain distance and also the transmission time and response time is more that is, less transmission speed.
  5) **Wi-fi module**:
A configured Wi-fi module  ESP32(NodeMCU package) or particle photon or Raspberry Pi is programmed  and connected in the PCB to the load through relays.
It has high transmission speed and high coverage area than Bluetooth medium.So , Wi-Fi communication technology is preferred for simple and energy efficient home automation from all the above ways.

In this design we use various sensors for various purposes and are connected in the PCB to the WiFi enabled microcontroller. Photosensor or LDR (light detecting resistor),smoke detector, temperature detector,Motion detection sensor,fire detector(smoke+heat) along with a buzzer and more. The microcontroller is connected to the router in the room that is the router acts as a central hub. The entire arrangement of microcontroller along with the relays is given supply from the mains and all the switches in the room will be replaced by two way switches. The light loads use electromagnetic relays and for heavy loads like AC, television etc., we use solid state relay.

This process  to print a PCB to integrate the various sensors to the microcontroller and connect them with the router. This provides various methods to operate the appliances apart from manual operation that will be through programmed sensors and through an app in the mobile phone connecting it's hotspot to the microcontroller. For this gateway checking the considerations 

1) Energy Efficient- Wi-Fi module provides fast transmission speeds and also consumes less energy and using automation technology the unnecessary consumption of electrical energy is reduced.
2) User Convenient- Sensors will automatically operaates as programmed reducing the user involvement along with this it can also be operated through a mobile.
3) Safety enhancements- The Wi-Fi module has its own SSID and password required for authenciation so the connectivity will be more secure.

   Using this module the equipment of the room which are choosen to automate are Windows and doors, Air conditioner, lights and fans,Fire alert system and fire extinguishers. As the operation is limited to a room and has more number of functions the module requires more number of GPIO pins. So we prefer using Particle photon that is Photon2 as the microcontroller.
   
The sensors along with their purposes and the basic structure of operation is as follows:
    1) Connecting each appliance with a related sensor of described requirement.
      Photosensor or LDR- Detects light and operates Windows and lights as programmed.
      PIR sensor- Detects motion and operates lights and fans
      Smoke and gas detectors- Detects smoke and harmful gases and operates windows and doors
      Temperature detection sensor- Detects the temperature and variations in temperature and operates AC, Windows and doors as programmed
    2) Collecting and analysing the data from each sensor 
    3) Operating relays and actuators based on the input data .

**BLOCK DIAGRAM and schematics**

![Photon2](https://docs.particle.io/assets/images/photon2-rendering.png)  

This is the actual Particle photon module and has the following features


1)802.11a/b/g/n Wi-Fi, 2.4 GHz and 5 GHz
2)Integrated PCB antenna
3)Integrated U.FL connector for external antenna
4)Integrated RF switch
5)BLE 5 using same antenna as Wi-Fi
6)Realtek RTL8721DM MCU
7)ARM Cortex M33 CPU, 200 MHz
8)2048 KB (2 MB) user application maximum size
9)3072 KB (3 MB) of RAM available to user applications
10)2 MB flash file system
11)FCC, IC, and CE certified

                       Block diagram of Photon2 
![Block diagram of Photon2](https://cdn.cnx-software.com/wp-content/uploads/2023/06/Photon-2-block-diagram-1396x1536.png?lossy=1&ssl=1)

                            schematic diagram 

![Design approach  (1)](https://github.com/Saitejasree18/Automation-SCRC/assets/75558225/21eeb2f1-aa32-4e1d-a5f7-045c1a18390e)



**COMPONENTS SPECIFICATION**

The entire arrangement is connected to the supply mains that is 230V AC so as per the microcontroller requirments the voltage is reduced to 3.6 to 5.5V of DC using stepdown transformer and rectifier from 

1) A Particle photon2  Wi-Fi Configured module
2) 5V relays for light loads and HVAC or 24V Dc relays for heavy loads
3) LDR or Photo sensor
4) PIR sensor
5) BTS7968 module or motor drive
6) Flame sensor-KY-026
7) Temperature sensor-LM35
8) Buzzer
9) Smoke or Gas detector-MQ-02
10) gears
11) DC 24V brushless motor


**DATAFLOW DIAGRAM**
![image](https://github.com/Saitejasree18/Automation-SCRC/assets/75558225/0f78d37f-14de-4bc5-bc5b-0b6c7388fb15)
The Data flow is seamless in this method because of easy connectivity 



