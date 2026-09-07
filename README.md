# Q²-Logic
Model and Library Documentation

## Models:
| | <ins>Q²-Logic</ins> | <ins>Q²-Logic Mini</ins> |
| :--- | :---: | :---: |
| **Supply voltage** | *12-24VDC* | *12-24VDC* |
| **Input** | *6* | *6* | 
| **Relay output** | *4* | *2* |
| **MOSFET output** | *4* | *4* |
| **Interface** | *USB-C, Wifi, CAN, RS485, I²C* | *USB-C, Wifi* |
> [!NOTE]
> Relay: *5A/ch | 250VAC*\
> MOSFET: *5A/ch, or max:15A (all chanel) | 30VDC*
>> Maximum temperature at full load: 70 °C

> [!WARNING]
> Do not exceed the maximum rated current, as this may damage the controller!

---

<details>
<summary><strong><ins>Q²-Logic</ins></strong>
- Click for a detailed description.</summary>

###
> **Core:** ESP32-S3\
> **Board size:** 102x86mm\
> **Input voltage:** 12-24VDC\
> -Minimum: 10V\
> -Absolute maximum: 30V\
> -Reverse voltage protected\
> -DC/DC converter IC ESD rating: 2 kV HBM (component level)\
> **Input current:** 800mA\
> **6 isolated digital inputs**\
> -Input voltage between COM and each input: 10–24 VDC\
> **4 relay output**\
> -Maximum load current: 5A 250VAC | 1A 30VDC
> **4 N-type MOSFET output**\
> -Maximum load current: 5A/CH or 15A(all chanel)\
> -Maximum voltage: 30VDC\
> -PWM frequency: 1,2kHz\
> 






![Q²-Logic Mini](images/3D_Q2-Logic_PCB.png)


</details>





























---

<details>
<summary><strong><ins>Q²-Logic Mini</ins></strong>
- Click for a detailed description.</summary>

</details>

---

# Library install

The Q²-Logic library is included in the board package and does not need to be installed separately.

1. Open **Arduino IDE**.
2. Go to **File → Preferences** and add the following URL to **Additional Boards Manager URLs**:

   ```text
   https://raw.githubusercontent.com/Build-Electric-Kft/Q2-Logic/main/package_q2_logic_index.json
   ```

3. Open **Tools → Board → Boards Manager**.
4. Search for **esp32** and install **esp32 by Espressif Systems**.
5. Search for **Q²-Logic Boards** and install the package.
6. Select **Tools → Board → Q²-Logic**.
7. Select the connected controller under **Tools → Port**.

The Q²-Logic API is now available in your sketch without an additional `#include`.

## Library functions

Call ` System.start()` in `setup()` before using the inputs and outputs.

### System

- **`System.start()`**  
  Initializes the inputs, switches all outputs off, and starts serial communication at 115200 baud.

- **`System.start(timeout_ms)`**  
  Performs initialization and enables the task watchdog when `timeout_ms` is at least 100 milliseconds.

- **`System.wdt_rst()`**  
  Feeds the watchdog. Call it regularly when the watchdog is enabled.

- **`System.restart()`**  
  Restarts the controller.

- **`System._isStarted()`**  
  Returns whether initialization has completed. Intended for internal library use.

### Inputs

Available on `I1` through `I6`. Examples below use `I1`.

- **`I1.read()`**  
  Returns the current input state: `1` when active, `0` when inactive. No debounce delay.

- **`I1.read(NO)`**  
  Reads the input using normal logic, comparing two samples taken 50 ms apart. If they differ, returns the last accepted state.

- **`I1.read(NC)`**  
  Uses the same filtering as `read(NO)`, but returns the inverted state.

> [!NOTE]
> `read(NO)` and `read(NC)` each block program execution for approximately 50 ms.

### Outputs

Available on `Q1` through `Q6`. Examples below use `Q1`, except for PWM.

- **`Q1.on()`**  
  Switches the output fully on and cancels any active pulse timer.

- **`Q1.off()`**  
  Switches the output off and cancels any active pulse timer.

- **`Q1.onPulse(duration_ms)`**  
  Switches the output on, then off after the specified duration. Does not block program execution.

- **`Q1.offPulse(duration_ms)`**  
  Switches the output off, then fully on after the specified duration. Does not block program execution.

- **`Q3.pwm(value)`**  
  Sets the PWM duty cycle from `0` (off) to `255` (fully on), at 1200 Hz. Cancels any active pulse timer.

- **`Q1.read()`**  
  Returns the stored output setting: `0` for off, `255` for fully on, or the PWM value. This is not physical output feedback.

> [!IMPORTANT]
> On the Mini, PWM is available on MOSFET outputs `Q3`–`Q6`.
> For relay outputs `Q1` and `Q2`, `pwm(0)` switches off and any nonzero value switches fully on.

> [!NOTE]
> Pulse durations are specified in milliseconds. A duration of `0` has no effect.
> A new pulse replaces the previous pulse timer on the same output.
> When a pulse ends, it switches to the opposite state; it does not restore the previous PWM setting.


