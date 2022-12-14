# Nodal-Analysis-and-Regulation-Circuit-NARC-

DISCLAIMER: Development work was versioned internally, this is the final version of my contributions to the project. All sensitive data/code has been removed and I 
received permission from my supervisors prior to publishing this.

Design objective: Protect edge computer from transient voltage spikes up to ~200V and report full excursion event to database via MQTT with EC acting as broker.

Included below is a diagram of the final PCB used in conjunction with the board (ESP32). Voltage was measured via a high-resistance divider to scale voltage down to Analog I/O acceptable levels. A hall-effect current sensor for the DC line was used instead of a resistor shunt due to greater efficiency and less risk of overvolting the second Analog I/O pin. Edge Computer overvoltage management was conducted via relay and a capacitor-driven UPS was included in the board as well to retain MCU operation in the advent of system shutdowns due to overvoltage-induced disconnects. I should clarify that I did not directly design/CAD most of the components used in the PCB but I was responsible for much of the overall board layout planning and dictation of design requirements, primarily via the suggestion of a capacitor-based UPS; I played a significant role in the UPS design via assesment of microcontroller compatibility and determination of target specifications for the device, including calculations for UPS capacitance and voltage tolerance. I also designed, built and tested simple perfboard prototype UPS designs early on as a proof-of concept.

![pm](https://user-images.githubusercontent.com/62817066/207215054-6325a705-9be0-4183-b9c1-6a432b17dace.PNG)

We decided to take advantage of the ESP32's dual-core architecture to implement a symmetric multiprocessing approach to networking and measurement collection. In addition to an improved sampling rate, the shared FIFO structure in this approach allowed us to 'queue up' fully captured excursion events for publishing during disconnect periods while still retaining ability to take ongoing measurements and record new events.

The pictures below show the firmware control flow and the MQTT networking approach implemented respectfully. Dynamic re-configuration details are available in the .README file in the src folder

![fwLoop](https://user-images.githubusercontent.com/62817066/207207799-215c1a16-aaea-4c58-893d-5b96a06b81b5.PNG)

![netSnip](https://user-images.githubusercontent.com/62817066/207207844-887dbe89-953f-4aeb-beba-219463f6eac3.PNG)


