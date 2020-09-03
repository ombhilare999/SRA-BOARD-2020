# SRA BOARD 2020

Compare to the 2019 means last year's SRA board there are some major changes done in new board design. All changes are mentioned here in greater detailed.

![](/Documentation/assets/boards_compare.png)


## What is development board ?

<p align="center">
  <img width="460" height="300" src="https://github.com/ombhilare999/SRA-BOARD-2020/blob/master/Documentation/assets/sra_board_2019.png">
</p>

In general every development board like sra board have following basic features:

- ### Power supply unit:
  - Microcontroller usually runs on 3.3V or 5V and input to the development board is normally 12V because of the motors.
  - So every development board has a power section which converts 12V to standard levels like 5V/ 3.3V for microcontroller and Sensors.
  - In previous year SRA board 12V to 5V was converted using LM7805 linear regulator. Using this 5V esp32 was powered.
  - Further this 5V was converted to 3.3V using LD33 linear voltage regulator. This 3.3V then given to the sensor port.

- ### Motor Driver:
    - Motors usually runs on 12V and microcontroller output is generally 5V/3.3V. So one need external motor driver circuitry to control motors according to the microcontroller input.
    - In sra board 2019 the motors was controlled using L298N motor driver which is a transistor based H Bridge motor driver.

- ### Sensor port:
    - According to the external sensor types usually development boards have on board sensor ports where sensor can be connected easily using FRC port.
    - Sra board 2019 contains two port for sensors. One port for LSA (line sensor array) and second port is for MPU6050.

- ### Protection against reverse voltage and overcurrent:
    - In sra board 2019 diodes are used in power line for reverse voltage protection.
    - And for the overcurrent protection of microcontroller and motor driver circuit fuses of 300mA and 3Amp are used respectively.

- ### Programmable switches and leds:
    - In general every development board should have some programmable switches and led for testing and control purpose.
    - So sra board 2019 consist of two programmable switches with two programmable leds.

- ### Power on/off switch:
    - Sra board 2019 has power switch for motor driver using which power supply to motor driver can be turned on or off.
    - Similarly there is a MCU switch for esp32 microcontroller using which microcontroller can be turned on or off.

>Now that you understood about basic of development board now let's talk about changes made in the new design.(for more detailed info of sra board 2019 checkout this [pdf]())

- ## Major changes made in the new design:
    - **7805(5V linear regulator) replaced by [LM2596 buck](https://www.youtube.com/watch?v=m8rK9gU30v4) circuit:**<br /><br />
     > - The reason of changing to buck circuit rather than using simple 7805 is the efficiency, output current and reliability of LM2596 is more than 7805.
     > - The efficiency of LM2596 is upto 92% which is way better than 7805. The LM2596 can provide current upto 3 Amp so from now on servos in ros workshop can be run using on board regulator itself.

    - **LD33(3.3V) replaced by AMS1117**:<br /><br />
    >  - Until last year we were using LD33 to convert 5V to 3.3V but after talking to our super senior we have decided to shift to more compact, reliable AMS1117(SOT-23) linear voltage regulator. (same voltage regulator i.e. AMS1117 is used on esp32 devkit c V4 module)

    - **L298N replaced by [TB6612FNG](https://dronebotworkshop.com/tb6612fng-h-bridge/)**:<br /><br />
    > - L298N is a bjt based H bridge motor driver but it is less efficient as compare to the new mos based TB6612FNG.
    > - Detailed comparison show below. As you can see the efficiency of TB6612FNG can reach up to 91-95% which is way higher than compare to the 40-70% efficiency of L298N.
     > - The only drawback of TB6612FNG is less continuous current which is equal to 1.2 Amp. So for higher current capacity motors two TB6612FNG are given on the board. so they can be used in parallel mode to double the current capacity to 2.4 Amp.
    
    <p align="center">
        <img width="460" height="300" src="https://i1.wp.com/dronebotworkshop.com/wp-content/uploads/2019/12/TB6612-vs-L298N.jpeg?w=768&ssl=1">
    </p>


    - **4 motor channels and normal, parallel mode of motor driver**:<br /><br />
    > -  In previous year sra board one L298N was used using which only two motors as l298n as two motor channels but in this year 2x TB6612FNG  motor driver is used so maximum 4 motors can be controlled using esp32.
    > - Motor driver can be worked in two modes **Normal mode** and **parallel mode**:   
    > > 1. **Normal Mode**:<br />
    ![](/Documentation/assets/normal_mode.png)<br />
    As discussed earlier in new design there are two motor drivers. Each TB6612FNG can control two motors. So therefore using two motor driver one can control 4 motors using 8 GPIO's of esp32.<br />
    For example: if 32 pin is HIGH(IN1 = HIHG) and pin 33 is low(IN2 = LOW) then motor 1 moves in the forward direction. <br \>
    So in normal mode 4 motors can be connected to the board.

    > > 2. **Parallel Mode**:<br />
    
    - **Shifting back to vintage Bar Graph LED and more switches**:<br /><br />
    > - In previous year we were using 2 programmable switches and 2 programmable Leds but in this years design we have provided bar graph led which contains 10 Leds out of which two are reserved for 5V and 3.3V voltage indication purpose.
    > -  So there are 8 programmable leds on the board. These leds multiplexed with directional pins of two motor driver to save pins.
    > -  What are directional pins ? >> Every motor driver channel has two directional pins IN1, IN2. If IN1 is high and IN2 is low then motors move in clockwise direction and there are 4 channels on the board so 4*2 = 8 diretional pins are multiplexed with 8 programmable leds)
    > -  With 8 leds in hand programmer can do crazy tricks for debugging. Some examples are as follows:
    > > 1) According to the lsa data we can program 4 leds to turn on when line sensor detects white color and turn off for black color with this feature debugging will be easy.
    > > 2) If motor is moving in forward direction according to that dedicated leds will be turn on indicating IN1 is high and IN2 is low because of this motion of the bot can be debugged.





