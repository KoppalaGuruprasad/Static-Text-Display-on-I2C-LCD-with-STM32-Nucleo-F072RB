# Static-Text-Display-on-I2C-LCD-with-STM32-Nucleo-F072RB
This repository contains a complete **STM32CubeIDE** project that interfaces a **16x2 LCD (HD44780)** via an **I2C backpack (PCF8574)** using the **STM32 Nucleo-F072RB** board.
The project displays multi-line text such as **"Hello World!"** using a custom I2C LCD driver.



## Features

* Fully working **I2C LCD driver (`i2c_lcd.c`)**
* LCD initialize, clear, cursor position, and print functions
* Works with any **16x2 / 20x4 LCD + I2C backpack (PCF8574)**
* Configured using **I2C1** (default pins: PB6 – SCL, PB7 – SDA)
* Clean HAL-based implementation
* Ready to compile & flash in **STM32CubeIDE**



##  Hardware Required

| Component                         | Description             |
| --------------------------------- | ----------------------- |
| **STM32 Nucleo-F072RB**           | Main MCU                |
| **16x2 LCD + PCF8574 I2C module** | I2C LCD                 |
| Jumper wires                      | for SCL/SDA connections |
| USB cable                         | to flash STM32          |



##  Wiring Connections (I2C)

| LCD I2C Module | STM32F072RB Pin |
| -------------- | --------------- |
| **SCL**        | PB6 (I2C1_SCL)  |
| **SDA**        | PB7 (I2C1_SDA)  |
| **VCC**        | 5V              |
| **GND**        | GND             |



##  Project Structure

```
LCD/
 ├── Core/
 │   ├── Inc/
 │   │   ├── i2c_lcd.h       <-- LCD driver header
 │   │   ├── i2c.h
 │   │   └── main.h
 │   ├── Src/
 │       ├── main.c          <-- LCD initialization & display text
 │       ├── i2c.c
 │       ├── i2c_lcd.c       <-- LCD driver implementation
 │       └── gpio.c
 ├── Drivers/
 ├── LCD.ioc                  <-- CubeMX configuration
 └── .project / .cproject     <-- STM32CubeIDE project files
```



##  How the Code Works

###  LCD Initialization

```c
lcd_init();
```

### ✔ Set Cursor + Print Text

```c
lcd_put_cursor(0,0);
lcd_send_string("Hello World!");

lcd_put_cursor(1,0);
lcd_send_string("From STM32Nucleo");
```

###  Driver Supports:

* Clear screen
* Cursor positioning
* Print string
* Send command / data
* Backlight control (if supported)



##  Build & Flash Steps

1. Open **STM32CubeIDE**
2. Go to: **File → Import → Existing Projects into Workspace**
3. Choose the `LCD/` folder
4. Build (`Ctrl + B`)
5. Connect STM32 board via USB
6. Click **Run → Debug** or **Run**

The LCD will immediately display the test messages.



##  Default I2C Configuration

| Parameter           | Value                           |
| ------------------- | ------------------------------- |
| **I2C Peripheral**  | I2C1                            |
| **Clock Speed**     | 100 kHz (standard mode)         |
| **Address Mode**    | 7-bit                           |
| **LCD I2C Address** | `0x27` (common PCF8574 address) |

> If your module uses **0x3F**, update it in `i2c_lcd.c`.



##  Example Output

```
Hello World!
From STM32Nucleo
```


