
Programmet starter ADC-konvertering på pin **PA3 (ADC1_IN3)**, leser den digitale verdien (0–4095), regner den om til spenning (0–3.3 V), og beregner temperaturen ut fra formelen:
[
T = (V - 0.5) \times 100
]
Resultatet skrives ut hvert sekund over UART i formatet:

```
sensorVal: 932, sensorVolt: 751 mV, temperature: 25.1 grader
```

**Hovedkomponenter i koden:**

* `MX_ADC1_Init()` – konfigurerer ADC (12-bit, enkeltkanal, software trigger)
* `MX_USART3_UART_Init()` – setter opp UART med 115200 baud
* `while(1)` – hovedløkke som kontinuerlig:

  1. Starter ADC-konvertering
  2. Leser resultatet
  3. Konverterer til spenning og temperatur
  4. Sender tekst via UART
  5. Venter 1 sekund