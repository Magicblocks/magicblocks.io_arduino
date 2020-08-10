*********************
What is Magicblocks?
*********************

.. image:: Images/magic.jpg
The Internet of things is nothing new. It is an evolutionary next step in the machine to machine communication paradigm. With an ever increasing number of 'things' at our disposal the need for connected 'things' has grown rapidly. However with increasing options comes added complexity which introduces steep learning curves and more importantly more confusion. What devices should I use? What cloud platform will best server my interest? I am new to IoT where should I start? Those are the question that would linger in any one who would dare to wonder in to the internet of Things. We, at magicblocks.io have put some magic to work to make the life of both the newcomer and the professional one step easier.

magicblocks.io is a launchpad for learning and prototyping your internet of things. It consists of
- Hardware suite made up of
		- Development boards
		- Prototyping kits for sensors & actuators
- Cloud platform made up of
		- Drag and drop editor to easily cook up your solutions
		- Dashboards to visualize your data
		- Data storage

Everything has been designed to make the learning curve as shallow as possible for the newcomer and as flexible as possible for the advanced user. 

**********************
Getting started
**********************

Setting up magicblocks
=======================

Sign Up & Login
---------------
- Visit `magicblocks.io <http://magicblocks.io>`_  and click signup at the top. 
- After filling the details and subnmitting you will get the activation link via email. Click on the link to activate the account. 
- Once done, you can login to your account from `magicblocks.io <http://magicblocks.io>`_ 

Start the Playground
---------------------

When you login for the first time your playground will not be running. Playground is the visual programming environment based on Node-Red that has been customized for seamless integration with hardware devices to enable IoT. If you do not have a valid subscription, you will be allowed to run the playground only for 1 hour continuously before it is automatically stopped. You will need to restart the playground manually after this 1 hour period

.. image:: Images/playgroundview.png
.. image:: Images/playgroundview-demomode.png

Setting up a device
====================

ESP32 based development boards
-------------------------------
- Install Arduino core for ESP32. Follow the instructions on ` official arduino core for ESP3 <https://github.com/espressif/arduino-esp32>`_
- Clone the ` ESP32-Magicblocks library <https://github.com/Magicblocks/ESP32-Magicblocks>`_ to your Arduino libraries folder
- Create a new project and past the code below:
.. code-block ::c

#include "ESP32_MB_Core.h"
unsigned long lastPing=0;
ESP32_MB_Core device;

void setup(){
  device.init();
}

void onCustomPayload(char* payload,int length){
  Serial.println("Payload received!");
  Serial.println(payload);
}

void loop(){
  device.loop();
  if(millis()-lastPing>10000){
    lastPing=millis();
    device.sendPayload("HELLO",5);
  }
}

- Upload to your ESP32 board
