# Nimbus-Air

**A little cloud that watches your air.** Nimbus-Air is a desktop air quality monitor that glows to show how healthy the air in a room is. It tracks temperature, humidity, VOCs and, on the Pro version, true CO2 and ambient light. Check it at a glance, from a browser over USB, or from your phone over Bluetooth.

> Nimbus-Air is a personal project by [KatanaByte](https://github.com/KatanaByte), built on the open-source **[AirCube](https://github.com/StuckAtPrototype/AirCube)** by StuckAtPrototype. See [Credits and license](#credits-and-license).

<!-- PLACEHOLDER: add a photo of your Nimbus-Air here, e.g. ![Nimbus-Air](docs/images/nimbus-air.jpg) -->

**[Nimbus-Air Web](https://katanabyte.github.io/Nimbus-Air/)**: live readings, history and firmware updates in your browser over USB. Nothing to install.

**[Nimbus-Air Phone](https://katanabyte.github.io/Nimbus-Air/phone/)**: live readings, history and brightness over Bluetooth. On iPhone, open it in the free **Bluefy** browser app; on Android or a computer, use Chrome.

---

## Getting started

**1. Plug it in.** Connect a USB-C cable to any USB port or charger. It powers on automatically.

**2. Wait for warm-up.** The air quality sensor needs about 3 minutes to settle after power-on. On the very first power-on of a new sensor, allow about **1 hour**.

**3. Read the glow.** Once warmed up, the color tells you the air quality:

| Glow | Air quality |
|------|-------------|
| Green | Good |
| Yellow | Moderate |
| Orange | Poor |
| Red | Bad: open a window |

The color shifts smoothly as conditions change.

**4. Adjust brightness.** Short-press the button to cycle brightness, or use the phone or web app.

No accounts, no cloud, no Wi-Fi.

---

## Base vs. Pro

Both versions use the ScioSense ENS161 for VOC Level, eCO2 and eTVOC. The Pro adds a direct CO2 sensor and automatic dimming.

| Feature | Base | Pro |
|---------|------|-----|
| VOC Level, eCO2 and eTVOC | ENS161 | ENS161 |
| Temperature and humidity | ENS210 | Sensirion SCD41 |
| True CO2 | No | Sensirion SCD41 (NDIR) |
| Ambient light | No | VCNL4040 |
| Automatic LED dimming | No | Yes |
| What drives the glow | VOC Level | Whichever is worse: VOC Level or true CO2 |

> **eCO2 vs. true CO2:** eCO2 is an estimate based on detected VOCs. The Pro's SCD41 measures CO2 directly, while the ENS161 still catches odors and fumes a pure CO2 sensor can miss.

## What it measures

| Measurement | Range | What it tells you |
|-------------|-------|-------------------|
| **VOC Level** | 0 to 500 | Volatile organic compounds scored on fixed indoor-air bands |
| **eCO2** | 400 to 65,000 ppm | Estimated CO2, derived from VOCs |
| **CO2** (Pro) | 400 to 5,000 ppm | True CO2, measured directly |
| **eTVOC** | 0 to 65,000 ppb | Total volatile organic compounds |
| **Temperature** | | Room temperature |
| **Humidity** | 0 to 100% | Relative humidity |
| **Illuminance** (Pro) | | Ambient light in lux; also dims the glow automatically |

### VOC Level bands

| Rating | Glow | VOC Level | TVOC (ppb) |
|--------|------|-----------|------------|
| Excellent | Green | 0 to 15 | 0 to 65 |
| Good | Green to lime | 15 to 50 | 65 to 220 |
| Moderate | Lime to yellow | 50 to 100 | 220 to 650 |
| Poor | Yellow to orange to red | 100 to 200 | 650 to 2,200 |
| Unhealthy | Red | 200 to 500 | 2,200 to 5,500 |

On the Pro, a CO2 Level score uses the same bands, and the glow shows whichever is worse.

---

## Button

| Action | What it does |
|--------|--------------|
| Short press | Cycle brightness (off, 10%, 30%, 60%, 100%) |
| Hold 3 seconds | Enter Zigbee pairing mode (glow flashes blue). The phone app can't connect in this mode. |

---

## Home Assistant

Nimbus-Air runs the AirCube firmware, so the original project's integrations work as-is:

- **Bluetooth:** by default it broadcasts standard **BTHome** data that Home Assistant can pick up with a Bluetooth adapter or ESPHome proxy.
- **Zigbee:** works with ZHA and Zigbee2MQTT. See the **[Home Assistant guide](HOME_ASSISTANT.md)**. It still identifies itself as "AirCube" over Zigbee.
- **SmartThings (community-contributed):** see **[SMARTTHINGS.md](SMARTTHINGS.md)**.

Custom Bluetooth clients: **[BLE GATT protocol reference](docs/BLE_GATT_PROTOCOL.md)**.

---

## Firmware

Current firmware: **v2.0.7** (stock AirCube firmware). Flash it from **[Nimbus-Air Web](https://katanabyte.github.io/Nimbus-Air/)**, or see the **[Firmware Update Guide](FIRMWARE_UPDATE.md)**.

All releases: **[Releases](https://github.com/KatanaByte/Nimbus-Air/releases)**

Building from source: see the **[Contributing Guide](CONTRIBUTING.md)** (ESP-IDF, target `esp32h2`).

---

## Desktop app (optional)

```
git clone https://github.com/KatanaByte/Nimbus-Air.git
cd Nimbus-Air/scripts
pip install -r requirements.txt
python aircube_app.py
```

---

## Assembly

You need the populated PCB, the printed case and three M2 x 5 mm self-tapping screws. Case files are in [`mechanical/base/`](mechanical/base) and [`mechanical/pro/`](mechanical/pro); see the **[Assembly Guide](ASSEMBLY.md)**.

<!-- PLACEHOLDER: link your own case design here once it's ready. -->

---

## Troubleshooting

**Glow doesn't turn on**
- Check the USB-C cable and power source; try another port or charger.

**Readings seem off right after power-on**
- Normal. Allow 3 minutes (about 1 hour on the very first power-on).

**Computer doesn't detect it**
- Some USB-C cables are charge-only. Use one that carries data.
- Windows may need [USB drivers](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers).

**Phone app can't find it**
- Make sure it isn't in Zigbee pairing mode (flashing blue).
- On iPhone, use the Bluefy app; Safari doesn't support Bluetooth web pages.

---

## Roadmap

<!-- PLACEHOLDER: edit as you go. -->

- [x] Rebrand web app and phone app to Nimbus-Air
- [ ] Change the Bluetooth name in firmware to Nimbus-Air
- [ ] Design my own cloud-themed case
- [ ] Redesign the web dashboard layout
- [ ] Rename Zigbee model identifier

---

## Credits and license

Nimbus-Air is based on **[AirCube](https://github.com/StuckAtPrototype/AirCube)** by **[StuckAtPrototype](https://stuckatprototype.com)**: the firmware, PCB design, enclosure, desktop app, web app and Home Assistant integrations all come from that project. If you want a ready-made unit, buy an [assembled AirCube](https://stuckatprototype.com/products/aircube) to support the original creator.

Nimbus-Air is not affiliated with or endorsed by StuckAtPrototype. "AirCube" is used here only to credit the original project.

**Changes in Nimbus-Air** (files changed are marked at the top):
- Web app (`web/`): renamed to Nimbus-Air; links point to this repo.
- Phone app (`web/phone/`): new Bluetooth app.
- Firmware release script (`scripts/build_web_manifest.py`): accepts Nimbus-Air release files.
- Site workflow (`.github/workflows/pages.yml`): renamed and pointed at the Nimbus-Air branch.

Licensed under the **[Apache 2.0 License](LICENSE)**, the same license as the original project.
