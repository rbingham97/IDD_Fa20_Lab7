# Video Doorbell

### Button Circuit

Done! 

(insert pic)

### Upload the `HelloYou` code

Done! The sketch works - the serial monitor shows an output of "light" when the button is pressed, then "dark" when it's released.

## Internet browsing on the Raspberry Pi

Cool! I particularly like the weather/moon information calls. 

## Serving webpages with the Raspberry Pi

** customize the code enough that the webpage served up is clearly your own, and include a screenshot and any modified code in the lab folder. **

I changed the text in basicserver to say "Hello Russell" instead of Hello world:

(insert image)

## Set up and Run Interaction Engine

For this exercise, we will set up and run HelloYou the basic Interaction Engine. This is like HelloWorld, but is called HelloYou because it is designed to be interactive and to connect actions and responses across distance.

![](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/blob/2020Fall/images/IxE_Explanation_python.gif?raw=true)

HelloYou has 3 parts:
1. The Arduino sketch, `helloYou.ino` that is installed and runs on the Arduino.
1. The Python code, `server.py`, that is installed and runs on the Raspberry Pi.
1. The html file and associated javascript code, `index.html` and `client.js`, which is served by the Raspberry Pi server to the client browser, and runs on the client’s computer.

### Flash the HelloYou Sketch onto the Arduino

**What messages are sent from the Arduino to the Pi? **

As noted earlier, the Arduino sends "light" when the button is pressed, then "dark" when it is released.

**What messages are expected from the Pi to the Arduino? **

In static/client.js, we see the messages sent and expected by the SocketIO framework. The server expects "light" and "dark" messages, just like the sketch sends. These messages turn the website background white and black respectively. The server also contains the JS functions that get called when a button is pressed, and these functions send tags to the python file that cause it to run its own functions that send either "H" or "L" to the Arduino. 

**What happens if the Pi sends an unexpected message to the Arduino? **

If the message is anything other than specifically the char 'H', the Arduino treats it the same regardless (the real message meant for this block is the char 'L'). Any other message results in the LED staying off. 

**How fast does the Arduino communicate with the Pi? What would you change to make it send messages less often? **

The Arduino sends one message every time the button state changes. To make this happen less often, we would add a counter or extra variable that measures when we actually want to send another message. 


### Run the HelloYou server on the RPi

**Look at the code. What interface does the Pi use to communicate with the Arduino when the code is running?**

The server code uses SocketIO to manage the messages that move back and forth between server.py and client.js. The server.py code communicates with the Arduino over serial. 

**What messages are sent from the Pi to the Arduino?**

The Pi sends either a 'H' or an 'L', based on whether a button is pressed on the website. 

**What part of the code controls what is served when a browser requests a page from the server?**

The index.html file is the first file queried by the browser -- this file then calls all the other files.

**What messages are sent to the console? When?**

Messages from the Arduino are printed to terminal, as are messages from the Pi. 


## Internet of Cornell Tech Things 

You will join a network of loosely networked Cornell Tech Things, which use the MQTT to communicate to one another. For the first step in this, we will build a simple client-server between your computer and your Interaction Engine. (Use the ``HelloThere`` and ``HelloFromHere`` code samples to do this!)

My MQTT client server is running and I can push colors to the TA LED. Haven't had time to finish the subscription code to take in colors from the server, but I'll do that in the next couple days. 

## Video doorbell

My video doorbell is done! I'll finish documenting it and push video and code when I finish the MQTT stuff, but it works just by pushing live video to the webpage whenever the Arduino senses a button press, then freezes the frame whenever the button is not pressed. 
