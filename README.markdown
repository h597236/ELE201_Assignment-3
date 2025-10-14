# ELE201 – Assignment 3  

## Table of Contents
- [Exercise 1: Temperature Sensor ADC and Serial Output](#exercise-1-temperature-sensor-adc-and-serial-output)
- [Exercise 2: Servo or DC Motor Control Using PWM](#exercise-2-servo-or-dc-motor-control-using-pwm)

---

## Exercise 1: Temperature Sensor ADC and Serial Output

### Objective
Read the analog voltage from a **TMP36 temperature sensor** connected to pin **PA3 (ADC1_IN3)**.  
Convert the ADC value into voltage and temperature (°C) and transmit the results once per second via **USART3** at 115200 baud.

### Features
- Single-channel ADC measurement (12-bit resolution)
- Converts ADC count → voltage → temperature  
  *Temperature (°C) = (Vout – 0.5) × 100*
- Sends formatted data over the serial terminal:
  ```
  sensorVal: 1234, sensorVolt: 1.12 V, temperature: 62.0 °C
  ```
- Updates every 1 second

### Pin Configuration
| Signal | MCU Pin | Function |
|---------|----------|--------------|
| TMP36 OUT | PA3 | ADC1_IN3 |
| USART3 TX | PD8 | UART output |
| USART3 RX | PD9 | UART input  |

### Circuit Diagram
```
                 STM32F767
               ┌───────────────┐
    TMP36_OUT ─┤ PA3  (ADC1)   │
               │               |
         GND ──┤ GND           │
         VCC ──┤ 3V3           │
               │               │
     UART_TX ──┤ PD8           │
     UART_RX ──┤ PD9           │
               └───────────────┘
```

### Expected Output
Open a serial terminal (115200 baud) and observe:
```
sensorVal: 2480, sensorVolt: 2.00 V, temperature: 150.0 °C
```

### Demo Video
[![Exercise 1 Demo](https://img.youtube.com/vi/VIDEO_ID_1/0.jpg)](https://www.youtube.com/watch?v=VIDEO_ID_1)

---

## Exercise 2: Servo or DC Motor Control Using PWM

### Objective
Use the STM32’s timer to generate a PWM signal on **PA6 (TIM3_CH1)**.  
The duty cycle or pulse width depends on an analog input read via **PA3 (ADC1_IN3)** or **PC0 (ADC1_IN10)**..

### Pin Configuration
| Component | MCU Pin | Function     | Notes |
|------------|----------|--------------|-------|
| Pot. Meter IN | PC0 | ADC1_IN10 | Analog input |
| TMP36 IN | PA3 | ADC1_IN3 | Analog input |
| Servo signal / Motor ENA | PA6 | TIM3_CH1 (PWM) | PWM output |

### Circuit Diagram (Servo example)
```
                 STM32F767
               ┌───────────────┐
TMP36         ─| PA3 (ADC1)    │
Pot. meter    ─| PC0 (ADC1)    │
Servo         ─┤ PA6 (TIM3)    │
               |               |
         GND ──┤ GND           │
        3.3V ──┤ 3.3V          |
       Servo ──┤ 5V            |
               └───────────────┘
```

### Demo Video
[![Exercise 2 Demo](https://img.youtube.com/vi/VIDEO_ID_2/0.jpg)](https://www.youtube.com/watch?v=VIDEO_ID_2)
