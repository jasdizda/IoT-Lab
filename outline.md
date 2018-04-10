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

Unit 1 - Offline LED blinking
-----------------------------

- Organization
- Getting to know the hardware & software
    - Let the students setup their code repository
    - Intro to the basics of lua and the NodeMCU programming
      model
    - Let them upload an LED-Blinking programm to the ESPs
    - Some easy adaption of the program to get used to the software
      like adding a button to toggle the LED

Unit 2 - Online LED blinking
----------------------------

- Let the students write a program that sends an UDP packet
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

Unit 3 - MQTT
-------------

- Show the differences between the previous client-server
  communication models and the MQTT broker based model
- Let the students write MQTT message consumers and producers
  like light switches & light fixtures

Unit 4 - Python & Async & MQTT
------------------------------

- Show the basics of the python language
- Show the basics of modern async/await
  concurrent programming
- Write an MQTT echo client that subscribes to one topic
  and publishes on another

Unit 5 - Python & Async & HTTP
------------------------------

- Show the basics of HTML, HTTP and forms
- Build a simple website that takes the status
  of a button using MQTT and displays it
- Build a website that allows changing the
  state of a lamp using an html form

Unit 5 - REST & JSON
--------------------

- Show the RESTful principle and how it maps
  to HTTP methods
- Adapt the server from the last unit to expose
  a restful interface

Unit 6 - CoAP
-------------

- Show the drawbacks of connection based protocols in
  resource constrained embedded applications
- Add an CoAP interface to the server from the
  previous unit

Unit 7 - Databases
------------------

- Show the basic functionality of an SQL database
- Show how an ORM like SQLObject can be used
  to simply add a database backend to a project
- Add a logging capability to the server
  from the previous unit
- Also add a user database and basic authentication

Unit 8 - TLS
------------

- Using packet dumps of the server from the previous
  unit show why data may not be sent unencrypted via
  the public internet
- Show the basics of public key cryptography and the
  certificate authority web of trust
- Generate a keypair for tls and get it signed by
  the tutor
- Use the signed certificate to add https to
  the server from the previous unit

Unit 9 - TLS & Secure password storage
--------------------------------------

- Put a root-of-trust certificate onto IoT device
  running NodeMCU
- Change the program on the IoT device to connect
  to the MQTT Broker using TLS

- Using a dump of the database file show why
  passwords may not be stored in plaintext
- Introduce the concept of password hashing
- Adapt the webserver program to use a password
  hashing library like passlib

Unit 10 - Data routing and aggregation
--------------------------------------

- Show that directly programming devices to publish/subscribe
  to fixed topics to communicate between them is unflexible
- Write a python program that links data sources and data sinks
  like e.g. mqtt topics
- "Dumb down" the NodeMCU programs to be simple
  producers/subscribers
- Add functionality to the python program to
  send aggregated reports to a server using HTPP REST

Unit 11, 12, 13 - Fog to Cloud project
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
