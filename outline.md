Hardware
========

- Reuse existing lab computers as student workstations
    - Build a Linux "Live-CD" with all of the software preinstalled
    - Do not allow any persistent storage on the computers to ease administration

- Use a Raspberry Pi 3 connected to some large screen as central server
    - Use on-board wireless chip to setup a WPA2-PSK WiFi for the Lab
      as the ESP8266 can not join Enterprise WPA networks like eduroam
        - Software: hostapd, dnsmasq
    - Setup a MQTT Server
        - Software: mosquitto
    - Setup CoAP server that forwards to MQTT
        - Software: something custom using python-aio
    - Setup a basic TCP and UDP server that signals
      activity via MQTT
        - Software: something custom using python-aio
    - Setup http{,s} server
        - To host teaching materials
        - To host a dashboard showing MQTT activity
        - To host something like gitlab to let the students store their programs
            - An external solution would be nicer but the university does
              not provide such a solution yet
    - Setup a browser to show the dashboard on the large screen

- Use ESP8266 modules running NodeMCU as IoT devices
    - NodeMCU uses lua for application code
        - Bad: One more programming language to learn
        - Good: Straightforward for anyone who knows
          C, Java or basically any language
        - Good: builtin modules for all the protocols
          and peripherals used
        - Good: Better debugging than native applications
    - Connect to the Raspberry Pi using WiFi

Content
=======

One semester allows for ~13 90min units.

Unit 1 - Introduction to the Lab: LED blinking in a LAN
-------------------------------------------------------

- Organization
- Part 1: Getting to know the hardware & software
    - Let the students setup their code repository
    - Intro to the basics of lua and the NodeMCU programming
      model
    - Let them upload an LED-Blinking programm to the ESPs
    - Some easy adaption of the program to get used to the software
      like adding a button to toggle the LED

- Part 2: Let the students write a program that sends an UDP packet
  to the server
    - The dashboard should display the metadata & payload of the packets
    - Adapt the program to send the packet upon
      the click of a button
    - Adapt the program to toggle an LED upon reception of an UDP packet
    - Controll the LED using a button in the dashboard
- Connect to the Server using TCP
    - Highlight the differences between UDP & TCP
        - Possibly using a package capturing tool like wireshark
    - Perform the same tasks as above
- Maybe also show Multicast and Broadcast UDP

Unit 2 - Communication protocols: MQTT
--------------------------------------

- Show the differences between the previous client-server
  communication models and the MQTT broker based model
- Let the students write MQTT message consumers and producers
  like light switches & light fixtures
- Show the basics of the python language
- Show the basics of modern async/await
  concurrent programming
- Write an MQTT echo client that subscribes to one topic
  and publishes on another
  
Unit 3 - Communication protocols: CoAP
--------------------------------------

- Show the drawbacks of connection based protocols in
  resource constrained embedded applications
- Add an CoAP interface to the server from the
  previous unit

Unit 4 - Communication protocols: REST HTTP & JSON using Spring
---------------------------------------------------------------

- Show the basics of HTML, HTTP and forms
- Build a simple website that takes the status
  of a button using MQTT and displays it
- Build a website that allows changing the
  state of a lamp using an html form
- Show the RESTful principle and how it maps
  to HTTP methods
- Adapt the server from the last unit to expose
  a restful interface

Unit 6 - Data Storage using Spring Framework
---------------------------------------------

- Show the basic functionality of an SQL database
- Show how an ORM like SQLObject can be used
  to simply add a database backend to a project
- Add a logging capability to the server
  from the previous unit
- Also add a user database and basic authentication

Unit 7 - mF2C project
--------------------------------------

- Each group is assigned a sensor/actor/routing/aggregation
  software component to work on.
- The components should form a home automation scenario
    - Ambient light sensor
    - Temperature & humidity sensor
    - Motion sensor
    - Current sensor for kettle / Washing machine
    - Light fixtures
    - Room Fan
- Data should be aggregated and forwarded to a cloud
  infrastructure
