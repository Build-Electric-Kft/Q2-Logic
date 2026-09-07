# Q²-Logic
Q²-Logic (Q2-Logic) is a family of ESP32-based programmable controllers developed by Build Electric Kft. This repository provides hardware specifications, Arduino board package installation instructions, and library documentation for Q²-Logic and Q²-Logic Mini.

## Models:
| | <ins>Q²-Logic</ins> | <ins>Q²-Logic Mini</ins> |
| :--- | :---: | :---: |
| **Supply voltage** | *12-24VDC* | *12-24VDC* |
| **Input** | *6* | *6* | 
| **Relay output** | *4* | *2* |
| **MOSFET output** | *4* | *4* |
| **Interface** | *USB-C, Wifi, Ethernet, CAN, RS485, I²C* | *USB-C, Wifi* |
> [!NOTE]
> Relay: *5A/ch | 250VAC*\
> MOSFET: *5A/ch, or max:15A (all chanel) | 30VDC*
>> Maximum temperature at full load: 70 °C

> [!WARNING]
> Do not exceed the maximum rated current, as this may damage the controller!

---

<details>
<summary><strong><ins>Q²-Logic</ins></strong> — Click for a detailed description.</summary>

### General specifications

- **Microcontroller:** ESP32-S3
- **Board dimensions:** 102 × 86 mm

### Power supply

- **Nominal input voltage:** 12–24V DC
- **Minimum input voltage:** 10V DC
- **Absolute maximum input voltage:** 30V DC
- **Reverse-polarity protection**
- **Input current:** 800mA
- **5V output:** maximum current 1A
- **DC/DC converter IC ESD rating:** 2kV HBM (component level)

### Digital inputs

- **6 isolated digital inputs**
- **Input voltage between COM and each input:** 10–24V DC

### Relay outputs

- **4 relay outputs**
- **Maximum switching current:**
  - 5A at 250V AC
  - 1A at 30V DC

### MOSFET outputs

- **4 N-channel MOSFET outputs**
- **Maximum load current:** 5A per channel, with a combined limit of 15A across all four channels
- **Maximum voltage:** 30V DC
- **PWM frequency:** 1.2kHz
- **Maximum temperature at full load:** 70°C

### Ethernet

- **Controller:** W5500
- **Link speed:** 10/100Mbps
- **Full- and half-duplex support**
- **Auto-negotiation**

### CAN bus

- Multi-master communication: any node can initiate transmission
- Built-in message arbitration and error detection
- Maximum node count depends on the transceivers and network configuration
- On-board 120Ω termination resistor
- Dedicated PESD1CAN TVS protection against ESD and voltage transients

### RS485

- Differential communication supporting multiple devices on a shared bus
- Master/slave operation depends on the protocol implemented in firmware
- Maximum node count depends on transceiver loading and protocol limitations
- On-board 120Ω termination resistor
- Dedicated PESD1CAN TVS protection against ESD and voltage transients

> [!NOTE]
> The PESD1CAN protection diodes are rated for 23kV contact discharge under IEC 61000-4-2. This is a component rating, not a verified ESD immunity rating for the complete board.
>
> Bus termination should be fitted at the two physical ends of each bus.

### I²C

- **Logic level:** 5V
- **Bus speed:** 100kHz Standard-mode / 400kHz Fast-mode
- **On-board EEPROM:** AT24C08C, 8Kbit (1KB) 7-bit I²C addresses: `0x50`–`0x53`
- **Level translator IC ESD rating:** 5kV HBM (component level)

### Board preview

![Q²-Logic](images/3D_Q2-Logic_PCB.png)

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


