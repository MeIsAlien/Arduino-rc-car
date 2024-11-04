# Remote Controlled Car based on Arduino and Infrared
This project by Joel Nadar demonstrates his journey to build a remote-controlled car using an Arduino Uno R3 and a TV remote.

### Hardware Required:
- Arduino Uno R3
- KY-022 IR sensor
- L298N motor driver
- 2 x DC BO motors with wheels
- 8 x 1.5V batteries
- 8 AA battery holder or 2 x 4 AA battery holder
- TV remote
- Sturdy rectangular hull(I used a paint board for this project)
- Double-sided tape
- Multimeter(optional but helped me a lot to figure out where the circuit was going wrong and how much power was directed to my motors)

### Step 1: mapping the right hex codes
Before we start wiring the entire thing together, let us first note down the hex codes that your TV remote/IR remote emits. We will be using these to map the right hex codes to the right commands.
```c++
#include <IRremote.h>

int RECV_PIN = 11;
IRrecv irrecv(RECV_PIN); 
decode_results results;

void setup() { 
	Serial.begin(9600); 
	irrecv.enableIRIn();
} 

void loop() { 
	if (irrecv.decode(&results)) {
		Serial.println(results.value, HEX); 
		irrecv.resume();
	}
	delay (100);
}
```
As of the time of testing, I was facing some issues with the latest version of IRremote(4.4.1), reverting back to version 2.8.0 solved the issue for me.
Make sure to note down the hex codes from the serial monitor.

### Step 2: Coding the Arduino and wiring everything together for testing
After we have noted the hex codes, we can upload them to the Arduino. Refer to main.iso for the code or simply copy paste it.

After having uploaded the code, we proceed to wiring all the components together. Note that all the components have to be wired in the following way inorder for it to work:
![circuit diagram](https://raw.githubusercontent.com/MeIsAlien/Arduino-rc-car/refs/heads/main/circuit_diagram.png)

If you have used a different wiring method, you will have to edit the code accordingly.

After this, you should test the circuit to check if the left and right motors turn according to the input given through your controller.

### Step 3: Assembling everything together
Now we need to assemble everything together.
For simplicity sake, I chose a 10x12 inch canvas paintboard that was left over from a previous project.
Mount the power supply, IR sensor, motor driver and the arduino on top of the hull and the two wheels under the hull such that one side is inclined towards the ground.
You may want to provide support to the front inorder to keep everything on the same level inorder to lessen the load on the wheels at the back. However, this is not necessary if the glue/screws you used to clamp the motor to the hull is strong enough. I used a packaging box inorder to support the hull on the front since I had used double sided tape to fix everything together.

It finally looked like this after it was all assembled together

https://github.com/user-attachments/assets/f01051e7-83c2-4c72-a04f-8ddc4e68a624



Note:
- Ensure that the power supply is sufficient to power all components, for me, one 9v battery was not enough to power it. I had to use 8 1.5v with 2amphour batteries to make it work efficiently.
- Experiment with different motor configurations and gear ratios to achieve desired performance.
- Refer to the specific datasheets of the components for detailed pinouts and usage instructions.
