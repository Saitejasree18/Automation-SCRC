# Automation-SCRC

DESIGN APPROACH

  The main theme is to design automation implementations for a room equipped with various electrical appliances and systems. Automation means making the operation easier and able to operate from anywhere. The goal of this project is to make every appliance automated and integrate them either with Wi-Fi or Bluetooth enabled microcontroller through cloud. This uses low-power Wireless communication protocols like Bluetooth ,Zigbee or LoRa to transmit data to the intermediate device such as embedded system hardware or a mobile phone and then uploads the data to the cloud server.Here we use Zigbee gateway as a centralized hub because of its less energy consumption compared to Wi-Fi and high range od connectivity compared to that of bluetooth. Zigbee is a mesh netwoek which has  three major components: Zigbee Coordinator,endpoints,Zigbee router.

  
   Automation of a Room can be done by both wired and wireless technology. In wired the control hub is connected to the switch board through relays and the operations of appliances is controlled using Assistants,External apps, and IR remotes. But I would like to approach this automation process by wireless connectivity using cloud computing. So, the basic design includes
   1) Connecting each appliance with a related sensor of described requirement.
      For Lights and fans- A PIR sensor is used to detect the motion and the data is sent to the cloud
      For Air conditioners- A temperature sensor LM35 or BC547 is used and using the data the temperature of air conditioner is adjusted
      For Windows- A light detection sensor and smoke detection sensor data controls the opening and closing of windows
      For fire alert system- A buzzer is operated when smoke detector and temperature sensor both were triggered on and the fire extinguishers are turned on
   2) Collecting the data from each sensor and got stored in the cloud.
   3) This data is given to the control hub and based on that the relays operate.
      
