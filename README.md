# Embedded Project 

This project implements a multi-mode embedded application on the **FRDM-MCXN947** board, using the **OLED display**, **LED array**, **Switches**, **Rotary Encoder**, **Potentiometer**, **DP Switches**, **Thermistor**, **Light Sensor**, and **Joystick**.  
The system is built as a **state machine**, with each state representing a mini-application activated through hardware inputs.  
Throughout the project, **timers** and **interrupts** are used extensively for control, synchronization, and event handling.   
`led_blinky.c` is the main code file.
`pin_mux.c` is the pin configurations file.

---

## 1. Initialization Phase

At system startup, the **NXP logo** (bitmap provided in `oled.c`) is displayed on the OLED.  
This boot logo appears only during the *initialization* stage for a few seconds before the application transitions to the main menu.


## 2. Main Menu

The OLED displays instructions for selecting one of the 4 sub-applications, based on the configuration of the **DP Switches**.

![Main Menu](media/main_menu.gif)

### **Available Sub-Applications:**



## 🛞 **DP1 – Rotate LEDs (SW direction change, ADC + Timer speed control)** 
🎥 ![App1 Demo](media/app1.gif)

**Description:**  
- LEDs rotate sequentially 🔄  
- Rotation direction changes when pressing a **switch (SW1)**  
- Rotation speed is controlled by the **potentiometer**, using **ADC readings** and a **hardware timer**

 

## **DP2 – Thermistor & Light Sensor Display**  
🎥 ![App2 Demo](media/app2.gif)

**Description:**  
- Reads ADC inputs from:  
  - Thermistor 🌡️  
  - Light sensor 💡   
- Timer interrupts ensure smooth sensor sampling and value display
- Temperature is taken as the ADC value


## **DP4 – Rotary Encoder LED Controller**  
🎥 ![App3 Demo](media/app3.gif)

**Description:**  
- Pressing the encoder button (SW6) turns **all LEDs ON** ✨  
- Rotating left or right gradually **turns off LEDs one by one** until one remains  
- The remaining LED then “moves” in the direction indicated by the encoder  
- Encoder direction is found by getting the current state of the encoder via **interrupts** and comparing it with the previous one
 

## 🕹️ **DP8 – Joystick-Controlled LEDs**  
🎥 ![App4 Demo](media/app4.gif)

**Description:**  
The LEDs light up based on joystick movement:  
- Up → Top LED ⬆️  
- Left → Left LED ⬅️  
- Right → Right LED ➡️  
- Down → Bottom LED ⬇️    

Joystick input is processed through ADC channels with interrupt-driven sampling.


## ⚠️ 3. Default Error State
![Error](media/error.gif)

Any unsupported DP Switch combination triggers the default error screen:


