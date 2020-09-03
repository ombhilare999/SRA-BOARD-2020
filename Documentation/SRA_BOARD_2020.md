# SRA BOARD 2020

Compare to the 2019 means last year's SRA board there are some majo/Documentation/assetshanges done in new board design. All changes are mentioned here in greater detailed.

![](/Documentation/assets/boards_compare.png)


## Background info of sra board 2019:

<p align="center">
  <img width="460" height="300" src="https://github.com/ombhilare999/SRA-BOARD-2020/blob/master/Documentation/assets/sra_board_2019.png">
</p>

In general every developement board like sra board have following basic features:

- ## Power supply unit:
  - Microcontroller usually runs on 3.3V or 5V and input to the developement board is normally 12V because of the motors.
  - So every developement board has a power section which converts 12V to standard levels like 5V/ 3.3V for microcontroller and Sensors.
  - In previous year SRA board 12V to 5V was converted using LM7805 linear regulator. Using this 5V esp32 was powered.
  -Further this 5V was converted to 3.3V using LD33 linear voltage regulator. This 3.3V then given to the sensor port.

- ## Motor Driver:
    - Motors usually runs on 12V and microcontroller output is generally 5V/3.3V. So one need external motor drive circuitry to control motors according to the microcontroller input.
    - In sra board 2019 the motors was controlled using L298N motor driver which is a transistor based H Bridge motor driver.

- ## Sensor port:
    - According to the external sensor types usually developement boards have on board sensor ports where sensor can be connected easily using FRC port.
    - Sra board 2019 contains two port for sensors. One port for LSA (line sensor array) and second port is for MPU6050.

- ## Protection against reverse voltage and overcurrent:
    - In sra board 2019 diodes are used in power line for reverse voltage protection.
    - And for the overcurrent protection of microcontroller and motor driver circuit fuses of 300mA and 3Amp are used respectively.

- ## Programmable switches and leds:
    - In general every developement board should have some programmable switches and led for testing and control purpose.
    - So sra board 2019 consist of two programmable switches with two programmable leds.

- ## Power on/off switch:
    - Sra board 2019 has power switch for motor driver using which power supply to motor driver can be turned on or off.
    - Similarly there is a MCU switch for esp32 microcontroller using which microcontroller can be turned on or off.



