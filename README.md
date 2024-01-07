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
6) Flame sensor(UV-IR type)
7) Temperature sensor-LM35
8) Buzzer
9) Smoke or Gas detector-MQ-02
10) mechanical gears
11) DC 24V brushless motor


**DATAFLOW DIAGRAM**

The Data flow is seamless in this method because of easy connectivity. In this method the data flow is from two ways:
  From sensors:  Sensors detect the change in parameter they are adressing and represent this with the change in voltage or current. This data is collected and transferred to the microcontroller. This is cross-checked with the programmed constraints and required action is performed for operating relays.
  ![Design approach  (2)](https://github.com/Saitejasree18/Automation-SCRC/assets/75558225/3e3695ea-a048-4ace-bcd6-510c159b0e53)

  From webpage: The input commands are considered from the programmed webpage are directed to the cloud. This command is given to the microcontroller from the cloud and it is directrd towards the required switch as per the given input.
  ![Design approach  (3)](https://github.com/Saitejasree18/Automation-SCRC/assets/75558225/1c3ed60c-c0f7-486f-9aa8-ceb9bcf428bc)


**EXECUTION APPROACH**

The specified design objectives are
1) Automation of lightning ,temperature and window controls
     For lightning:  The objective of this automation is to maintain sufficient lightning in the room. This is maintained using PIR sensor and LDR sensor. A wide range PIR sensor is used to detect the motion when a person enters the room and turns ON the light. The PIR sensor has three pins with groung and supply voltage and a digital output pin connected in the digital side of controller and in the program it is specified as if(PIR==1) then lights are turned ON.
    The brightness of the light is controlled based on the intensity of illumination on the LDR sensor which is measured in lux. The intensity is inversly proportional to the resistance so as the brightness of surroundings increases the switch is turned off. In such a case the lights connected to the LDR sensors are turned ON to maintain the required lightning which is defined in the program by specifying certain resistance. The room here is assumed to be equipped with three different lights one works with PIR and the remaining two are under two LDR sensors. It is programmed such that if the intensity is in between 100-400 lux one of them is turned ON and if it is greater than 400 lux both are turned off and if it is less than 100lux or in the late evening both are turned ON. 
    For temperature:  The objective is to maintain certain room temperature as per the humidity and temperature of the surroundings. We use LM35 sensor to detect the temperature. The room temperature for Indian weather conditions has to be maintained in between 25 to 32 degree celsius. This is given as threshold value to the sensor in the program .If the temperature value exceeds, the cooling mode of air conditioner is turned ON and if it is below the threshold value, the conditioning mode is turned ON by some HVAC relay. For any change in the temperature the AC is turned ON. It can also be connected to a fan and the fan either turned ON or OFF based on the temperature.
     Window Controls:  The objective is to open and close the window as per the sensor data. For maintaining required lightning and to allow the enough sunlight during dawn and dusk the windows are opened. This is done with the help of mechanical gears and brushless DC motor which is connected to the microcontroller board through a motor driver(BTS7968). The LDR sensor data is integrated to the operation of motor driver to close and open the door.
   In case of smoke detection the windows are allowed to open using smoke detector MQ-02 which triggers the motor driver when it detects any gases such as LPG,methane,alcohol,Hydrogen and smoke to close the window
   In case of fire in the room the windows should be closed to cutoff the oxygen supply. This can be done using a flame sensor which is basically a UV-IR photodiode that detects the flame and turns the digital output to 1 which turns the buzzer ON. This also locks the window.
2) Smart management of electrical appliances
   All the electrical appliances are integrated to a single microcontroller board through relays which are operated based on the sensor data. This reduces the manual operation to a great extent and the connectivity makes it easier to integrate all the devices to a single board. The power consumption of each appliance is reduced and the energy is consumed only when needed. This makes the system energy efficient and the wifi module used that is Particle Photon consumes less energy and has fast transmission speed so the response will be quick.
3) Integration of Fire alert system with other room systems
   The fire alert system is basically constructed using a UV-IR phototransistor which detects the UV and IR spectrum that is present in the flame. Using this data the buzzer is triggered ON which acts as fire alarm. This fire is integrated with the operation of windows and doors. The doors and windows are closed to cutoff the oxygen supply and to stop the flame to extend. Along with the buzzer the extinguishers also gets triggered to reduce the fire. With closing doors and windows and with the use of fire alarm the spread of fire to other rooms is stopped and gives an alert to them.
4) Enhanced Connectivity and control via routers
   Using Wi-Fi or routers for connectivity gives
   a) easy data flow
   b)fast transmission
   c)Secure system with a unique SSID and password
   d)can be operated by any means such as a mobile phone or a computer with the help of an app, applet or web application


**SPECIAL FEATURES/ADVANTAGES**

1) Using the cloud to store the sensor data helps to retrieve it if needed anytime
2) A Voice control app such as Alexa or Assistant can be integrated and make the operation more easier
3) It can be extended to connect more sensors and can allow their functioning at a time
4) This can also be connected to any mobile hotspot rather than  LAN ,WAN and router
5) This can be adopted to any existing technology such as 4G,5G and AI
6) Easy to install and consumes less cost
7) Easy to program as it has its own IDE

**JUSTIFICATION FOR EACH AUTOMATION CHOICE**

1) LDR sensor- Easy to connect,low cost,more sensitive to light
2) PIR sensor- Gives accurate detection,low power consumption,good range enough to serve in a room
3) UV-IR flame sensor- Had a good accuracy can easily detect even a small amount of flame and gives a digital output
4) Smoke and gas detection sensor(MQ-02)- Can detect multiple gases at an affordable cost and easily available,simple to use
5) LM-35 temperature sensor- gives accurate result with low power consumption, linear output
6) Particle Photon 2 as a control unit- Easy connectivity, easy adaptability and easily programmable gives free RTOS


**POTENTIAL BENEFITS AND IMPACTS**

BENEFITS
1) Accessibility
2) Energy-efficient so reduces running cost
3) Can be integrate with any smart device having internet access

IMPACTS
1)Though it has secured password the system is vulnerable to hacking and unauthorized access
2)In case of low signal or network outage, the system may not work
3)It is complex to setup and manage


**ASSUMPTIONS AND CONSIDERATIONS**

This is the basic automation that can be done using a Wi-Fi based module but it can improved in so many ways. 
1)The entire system can be connected a customised AI assistant such as jarvis to communicate without any medium using machine learning algorithms.
2)The system can be made secure by using encryption protocols and multi-factor authentication to access
3)The use of many sensors can be reduced by connecting many appliances to a single sensor which also reduces the cost
4)Along with the Wi-Fi router providing backup communication
5)Enabling multiple devices to operate the system at a time

  Zigbee communication technology is a way more faster,efficient and secure than the Wi-Fi or router connectivity but the major disadvantage is the mesh network. The Zigbee network is a mesh network such that the damage at one node may affect the entire system. 

  


  




