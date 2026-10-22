# BLDC-FOC-Motor-Driver

![Status](https://img.shields.io/badge/status-schematic%20in%20progress-orange)
![Hardware](https://img.shields.io/badge/hardware-rev%20A-blue)
![KiCad](https://img.shields.io/badge/KiCad-10-314CB0?logo=kicad&logoColor=white)
![MCU](https://img.shields.io/badge/MCU-STM32G431-03234B?logo=stmicroelectronics&logoColor=white)
![Gate driver](https://img.shields.io/badge/gate%20driver-DRV8323RH-CC0000)
![Firmware](https://img.shields.io/badge/firmware-not%20started-lightgrey)

Single-motor **BLDC / PMSM driver with Field-Oriented Control (FOC)**.
It's the motor-control building block for a two-wheeled self-balancing robot. It's also designed to work as a standalone driver on the bench, commanded over USB.

## Libraries

This project uses the shared KiCad libraries from L2-Hardware.

1. Clone the library repository **in the same parent folder as your project folders**, so that it sits next to them:

```bash
   git clone https://github.com/L2-Hardware/Kicad_Libs
```

   Expected folder structure:

```
   Kicad/
   ├── Kicad_Libs/
   ├── Project1/
   └── Project2/
   └── etc...
```

2. Inside the project folder, run the `bring_libs.bat` script to import the libraries into the project.

## Key specs

| | |
|---|---|
| Supply | 2S–6S LiPo (7–25 V), designed around 4S |
| Phase current | up to ~15 A peak (±16.5 A sense range) |
| Control | Sensored FOC, 20 kHz current loop |
| Position feedback | AS5047P 14-bit magnetic encoder, on-board, centred on the motor shaft |
| Interfaces | USB-C (config, telemetry, firmware update), SWD via Tag-Connect TC2030 |
| Logic supply | DRV8323 integrated buck → 5 V, LDO → 3.3 V; USB can power the logic for bench work |


## Main components

| Block | Part |
|---|---|
| MCU | STM32G431CBU6 (Cortex-M4F 170 MHz, CORDIC, FDCAN) |
| Gate driver | TI DRV8323RH (hardware config, integrated buck) |
| Power stage | 6× N-MOSFET 60 V, SON 5×6 |
| Current sensing | 3× 5 mΩ Kelvin shunt + TI INA240A1, inline on the phases |
| Encoder | ams AS5047P + diametral magnet |
| Protection | SMBJ26A TVS on VBAT, USBLC6-2SC6 ESD on USB, polyfuse + Schottky diode-OR on VBUS |



## Roadmap

- [x] Architecture and component selection
- [ ] Schematic: connectors ✅ · power ✅ · gate driver · inverter · current sense · encoder · MCU
- [ ] PCB layout (4 layers)
- [ ] Fabrication and assembly
- [ ] Bring-up: power rails, SWD, encoder, PWM and dead-time, current sense calibration
- [ ] Firmware: open loop → current loop → velocity/position loops
- [ ] Integration in the self-balancing robot

## Author

Lorenzo Dati
