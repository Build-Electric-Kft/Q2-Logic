# Q²-Logic
Arduino panelcsomag a Q²-Logic vezérlőkhöz.

## Verziók
**Q²-Logic Mini:** *(ESP32-C3 core)*

- *6 Bemenet*
- *6 Kimenet*
  - 2db Relé (5A/ch)
  - 4db MOSFET (5A/ch)
- Wifi

**Q²-Logic:** *(ESP32-S3 core)*

- *6 Bemenet*
- *8 Kimenet*
  - 4db Relé (5A/ch)
  - 4db MOSFET (5A/ch)
- CAN Bus
- RS485
- I²C
- Wifi

## Telepítés

1. Telepítsd az Espressif ESP32 Arduino core-t. Stabilan működő verzió: 
2. Add hozzá a következő URL-t az Arduino IDE további alaplapkezelő URL-jeihez:

   https://raw.githubusercontent.com/Build-Electric-Kft/Q2-Logic/main/package_q2_logic_index.json

3. A Boards Managerben telepítsd a **Q²-Logic Boards** csomagot.

## Példaprogramok
###cucc

```cpp
void setup() {
  System.start();
}

void loop() {
  if (I1.read()) {
    Q1.on();
  } else {
    Q1.off();
  }
}
```

## Letöltés

[A kiadások megnyitása](https://github.com/Build-Electric-Kft/Q2-Logic/releases)
