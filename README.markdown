# ELE201 – Assignment 3  
**Microcontroller Programming with STM32F767**

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
| Signal | MCU Pin | Function     | Notes                |
|---------|----------|--------------|----------------------|
| TMP36 OUT | PA3 | ADC1_IN3 | Analog input |
| GND | GND | — | Common ground |
| VCC | 3V3 | — | 3.3 V supply |
| USART3 TX | PD8 | UART output | ST-LINK VCP |
| USART3 RX | PD9 | UART input  | ST-LINK VCP |

### Circuit Diagram
```
                 STM32F767
               ┌───────────────┐
     TMP36_OUT ─┤ PA3  (ADC1)  │
          GND ──┤ GND          │
          VCC ──┤ 3V3          │
                 │              │
       UART_TX ──┤ PD8          │
       UART_RX ──┤ PD9          │
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
The duty cycle or pulse width depends on an analog input read via **PA3 (ADC1_IN3)**.

Two variants may be tested:

1. **Servo Control** – Potentiometer on PA3 sets the servo’s position.  
2. **DC Motor Control** – TMP36 temperature sensor on PA3 controls motor speed.

### Features
#### Option A – Servo Control
- PWM frequency = 50 Hz  
- Pulse width = 0.5 ms → 2.5 ms (full servo range)  
- Maps ADC (0–4095) → 500–2500 µs  
- Live serial printout of ADC and pulse width

#### Option B – DC Motor Control
- PWM ≈ 1 kHz (quiet operation possible up to 20 kHz)
- Duty cycle set by temperature:
  - ≤ 20 °C → 0 %  
  - ≥ 30 °C → 100 %
- Direction control via two GPIO pins (e.g. PB0 / PB1 for H-bridge)
- Serial output: temperature and PWM duty %

### Pin Configuration
| Component | MCU Pin | Function     | Notes |
|------------|----------|--------------|-------|
| Pot/TMP36 OUT | PA3 | ADC1_IN3 | Analog input |
| Servo signal / Motor ENA | PA6 | TIM3_CH1 (PWM) | PWM output |
| Motor IN1 | PB0 | GPIO_OUT | Direction |
| Motor IN2 | PB1 | GPIO_OUT | Direction |
| UART TX | PD8 | USART3 TX | Serial output |
| UART RX | PD9 | USART3 RX | Serial input |

### Circuit Diagram (Servo example)
```
                 STM32F767
               ┌───────────────┐
   Potentiometer ─┤ PA3 (ADC1) │
       Servo SIG ─┤ PA6 (TIM3) │
            GND ──┤ GND        │
            3V3 ──┤ 3V3        │
                 │              │
        UART_TX ─┤ PD8          │
        UART_RX ─┤ PD9          │
               └───────────────┘
```

### Serial Output Example
```
ADC: 3050, Pulse: 1880 µs
tempC: 25.3, duty: 53.0 %
```

### Demo Video
[![Exercise 2 Demo](https://img.youtube.com/vi/VIDEO_ID_2/0.jpg)](https://www.youtube.com/watch?v=VIDEO_ID_2)

---

## Tools / Environment
- **Board**: STM32F767 (Nucleo or Discovery)
- **IDE**: STM32CubeIDE / CubeMX (HAL drivers)
- **Language**: C (HAL API)
- **Baud Rate**: 115200 bps
- **Supply Voltage**: 3.3 V

---

## References
- ELE201 Lab 3 – Microcontroller I/O and PWM control  
- ST Microelectronics – STM32F7 Reference Manual  
- Analog Devices TMP36 Datasheet
