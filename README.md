# Q²-Logic

Arduino panelcsomag a Q²-Logic Mini vezérlőhöz.

## Telepítés

1. Telepítsd az Espressif ESP32 Arduino core-t.
2. Add hozzá a következő URL-t az Arduino IDE további alaplapkezelő URL-jeihez:

   https://raw.githubusercontent.com/Build-Electric-Kft/Q2-Logic/main/package_q2_logic_index.json

3. A Boards Managerben telepítsd a **Q²-Logic Boards** csomagot.
4. Válaszd ki a **Q²-Logic Mini** panelt.

## Példaprogram

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
