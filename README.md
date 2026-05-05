# Well Illumination System

The goal of this system is to provide independent and precise control of a 24-LED matrix composed of high-power LEDs. The architecture is divided into two main stages: two dedicated PCA9685 PWM controllers that handle 12 channels each, and individual power modules equipped with AL8861 components. 

## 1. 24-LED Control Board

### Power and Regulation Module
This module converts the main 12V input into a stable 3.3V supply to power the ESP32 microcontroller and the PCA9685 PWM drivers.

* **Regulator**: It uses a TSR1-2433E buck switching converter for high energy efficiency. 
* **Protection**: A D1 diode protects the circuit against reverse polarity. 
* **Diagnostics**: A green LED (D2) indicates when the system is powered. 

![Voltage Regulator Module Diagram]([IMAGE_PLACEHOLDER_REGULATOR])

### Microcontroller (ESP32)
The ESP32 executes the embedded program and transmits brightness instructions via I2C (SDA/SCL). Pull-up resistors (R1, R2) ensure stable data transmission. 

### PWM Drivers (PCA9685)
Two PCA9685PW chips generate 24 stable PWM signals at 400 Hz. 
* **Addressing**: Driver 1 (U3) is at 0x40; Driver 2 (U4) is at 0x41. 
* **Stability**: Decoupling capacitors (C3-C6) are placed close to the VDD pins.

### Constant Current LED Drivers (AL8861)
This power stage translates the PWM signals into constant current for the LEDs.
* **Efficiency**: Uses a Buck switching regulator to minimize heat.
* **Current Setting**: Nominal current is hardware-defined at 300 mA via a 0.33 Ω resistor (R4).

![AL8861 Driver Schematic]([IMAGE_PLACEHOLDER_DRIVER])

## 2. LED Plate
This secondary PCB houses the 24 high-power OSLON SSL 80 LEDs
* **Thermal Management**: Uses an **aluminum plate** instead of standard FR4 to dissipate intense heat. 
* **Geometry**: LEDs are arranged in a matrix with 19.5 mm spacing to align with the 24-well plate. 
* **Optics**: Convergent lenses are housed in a custom 3D-printed piece to focus light.

![LED Matrix Visual]([IMAGE_PLACEHOLDER_MATRIX])

## 3. Legacy Box UI (Bonus)
A 3D-printed box housing a legacy interface with a screen and rotary encoder to manually control brightness.

## Documentation & Links
* **General Git**: [science-jubilee](https://github.com/leosabatie-eng/science-jubilee) 
