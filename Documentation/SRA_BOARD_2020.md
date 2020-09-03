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

>Now that you understood about basic of development board now let's talk about changes made in the new design.

- ## Some of the major changes made in the new design:
    - **7805(5V linear regulator) replaced by [LM2596 buck](https://www.youtube.com/watch?v=m8rK9gU30v4) circuit:**
     > The reason of changing to buck circuit rather than using simple 7805 is the efficiency, output current and reliability of LM2596 is more than 7805. The efficiency of LM2596 is upto 92% which is way better than 7805. The LM2596 can provide current upto 3 Amp so from now on servos in ros workshop can be run using on board regulator itself.
    - **L298N replaced by TB6612FNG**:
    > L298N is a bjt based H bridge motor driver but it is less efficient as compare to the new mos based ![TB6612FNG](https://dronebotworkshop.com/tb6612fng-h-bridge/). Detailed comparison show below.
![](https://i1.wp.com/dronebotworkshop.com/wp-content/uploads/2019/12/TB6612-vs-L298N.jpeg?w=768&ssl=1)
    As you can see the efficiency of TB6612FNG can reach up to 91-95% which is way higher than compare to the 40-70% efficiency of L298N. the only drawback of TB6612FNG is less continuous current which is equal to 1.2 Amp. So for higher current capacity motors two TB6612FNG are given on the board. so they can be used in parallel mode to double the current capacity to 2.4 Amp.
    


