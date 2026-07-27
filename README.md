# 1 kW Pure Sine Wave Transformerless Inverter (60–84 V DC to 230 V AC)

A high-efficiency **1 kW Transformerless Pure Sine Wave Inverter** designed for battery-powered applications. The inverter converts a **60–84 V DC battery input** into a regulated **230 V AC, 50 Hz pure sine wave output** using a **two-stage power conversion architecture** consisting of:

- High-frequency Push-Pull DC-DC Converter
- Full-Bridge SPWM DC-AC Inverter

This project was designed to achieve high efficiency, reduced transformer size, improved power density, and reliable protection suitable for renewable energy systems, battery backup systems, and electric vehicle auxiliary power supplies.

---

# Project Specifications

| Parameter | Value |
|-----------|--------|
| Rated Power | 1 kW |
| Input Voltage | 60–84 V DC |
| Output Voltage | 230 V AC RMS |
| Output Frequency | 50 Hz |
| Output Waveform | Pure Sine Wave |
| DC Bus Voltage | 340 V DC |
| Isolation | High Frequency Push-Pull Transformer |
| Output Topology | Full Bridge (H-Bridge) |
| PWM Generation | SG3525 + EGS002 |
| Output Filter | LC Filter |
| Cooling | Temperature Controlled Fans |
| Protection | Over Voltage, Under Voltage, Over Current |

---
```text
                                                                      1 kW PURE SINE WAVE TRANSFORMERLESS INVERTER

┌──────────────────┐
│ 60–84 V Battery  │
└────────┬─────────┘
         │
         ▼
┌─────────────────────────────────────────┐
│ Input Capacitor Bank                    │
│ • 2 × 470µF Electrolytic Capacitors     │
│ • 2 × 100nF Film Capacitors             │
└────────┬────────────────────────────────┘
         │
         ▼

┌─────────────────────────────────────────────────────────────────────────────────────────────┐
│                         HIGH FREQUENCY BOOST CONVERTER (PUSH-PULL)                           │
│                                                                                             │
│  SG3525 PWM Controller                                                                      │
│          │                                                                                  │
│          ▼                                                                                  │
│  Totem Pole Gate Driver                                                                     │
│          │                                                                                  │
│          ▼                                                                                  │
│  Parallel MOSFET Push-Pull Switching Stage                                                  │
│          │                                                                                  │
│          ▼                                                                                  │
│  High-Frequency Centre-Tapped Ferrite Transformer                                           │
└───────────────────────────────┬─────────────────────────────────────────────────────────────┘
                                │
                                ▼

                  ┌──────────────────────────────────┐
                  │ High-Speed Bridge Rectifier      │
                  └───────────────┬──────────────────┘
                                  │
                                  ▼

                  ┌──────────────────────────────────┐
                  │        340 V DC Link             │
                  │      Bulk Capacitor Bank         │
                  └───────────────┬──────────────────┘
                                  │
                                  ▼

                  ┌──────────────────────────────────┐
                  │ Full Bridge Inverter             │
                  │ 4 × IRFP460 MOSFETs              │
                  └───────────────┬──────────────────┘
                                  ▲
                                  │
                  ┌───────────────┴──────────────────┐
                  │ EGS002                           │
                  │ SPWM Generator + Gate Driver     │
                  └───────────────┬──────────────────┘
                                  │
                                  ▼

                  ┌──────────────────────────────────┐
                  │ LC Low Pass Output Filter        │
                  └───────────────┬──────────────────┘
                                  │
                                  ▼

                  ┌──────────────────────────────────┐
                  │ 230 VAC RMS Pure Sine Output     │
                  └──────────────────────────────────┘


                        ───────────── FEEDBACK CONTROL ─────────────

            Output Voltage ───────────────────────────────► EGS002

            Output Current ───────────────────────────────► EGS002
                                     (5 A Current Limit)


                        ───────────── PROTECTION SYSTEM ─────────────

        Battery Voltage
               │
               ▼
      Voltage Divider Network
               │
               ▼
        LM393 Comparator
     (OVP / UVP Detection)
               │
               ▼
      Shutdown (SD) Pin
         of SG3525
               │
     ┌─────────┴──────────┐
     │                    │
     ▼                    ▼
 PWM Enabled       PWM Disabled
     │                    │
     ▼                    ▼
 Converter Runs     Converter Stops


                        ───────────── COOLING SYSTEM ─────────────

        Heat Sink Temperature
                  │
                  ▼
          NTC Thermistor
                  │
                  ▼
        Fan Control Circuit
                  │
        ┌─────────┴─────────┐
        ▼                   ▼
   Fan ON (>Threshold)   Fan OFF
```


# Stage 1 — Input DC Filtering

The inverter operates from a **60–84 V battery pack**.

To minimize voltage ripple and absorb high transient currents drawn by the push-pull converter, the battery input is filtered using:

- **2 × 470 µF / 160 V Electrolytic Capacitors**
- **2 × 100 nF / 160 V Film Capacitors**

### Purpose

### Electrolytic Capacitors

- Store energy during switching
- Reduce low-frequency ripple
- Supply instantaneous current
- Improve voltage stability

### Film Capacitors

- Filter high-frequency switching noise
- Reduce EMI
- Improve converter stability
- Suppress voltage spikes

The combination of large electrolytic and small film capacitors provides excellent filtering over a wide frequency range.

---

# Stage 2 — Push-Pull DC-DC Converter

The first conversion stage boosts the battery voltage to approximately **340 V DC**.

Topology Used:

- Push-Pull Converter
- Center-Tapped Transformer
- High Frequency Switching

### PWM Controller

An **SG3525 PWM Controller IC** is used to generate complementary PWM signals.

The SG3525 provides:

- Stable oscillator
- Adjustable duty cycle
- Dead-time control
- Soft start
- Shutdown input
- Error amplifier

These PWM signals drive the power MOSFET stage.

---

# Totem Pole Gate Driver

The output current capability of the SG3525 is insufficient to rapidly charge and discharge large MOSFET gate capacitances.

Therefore, a **Totem Pole Gate Driver** is used.

### Functions

- Amplifies gate drive current
- Faster MOSFET switching
- Reduced switching losses
- Lower heating
- Improved efficiency

The totem pole stage enables reliable operation of the parallel MOSFET configuration used in the push-pull converter.

---

# Push-Pull MOSFET Stage

Two power MOSFETs are connected in parallel on each switching side.

The MOSFETs alternately pull each half of the center-tapped transformer primary winding to ground.

This creates alternating magnetic flux in the transformer core, allowing efficient high-frequency power transfer.

Benefits include:

- Lower conduction losses
- Better current sharing
- Higher output power capability
- Reduced device heating

---

# High Frequency Center-Tapped Transformer

A custom-designed ferrite transformer is used.

Primary:

- Center tapped
- Connected directly to battery positive

Secondary:

- High-voltage winding
- Generates high-frequency AC

Advantages:

- Much smaller than 50 Hz transformer
- High efficiency
- Reduced weight
- High power density

---

# High Voltage Rectifier

The transformer's secondary output is rectified using a high-speed bridge rectifier.

Output:

**Approximately 340 V DC**

This high-voltage DC rail supplies the H-Bridge inverter stage.

---

# DC Bus

The rectified output forms a stable **340 V DC Bus**.

The DC bus acts as an energy storage stage before AC conversion.

Additional filtering capacitors reduce ripple and improve regulation.

---

# Stage 3 — H-Bridge Inverter

The second conversion stage converts the 340 V DC bus into a pure sine wave AC output.

Topology:

Full Bridge (H-Bridge)

MOSFET Used:

**IRFP460**

The H-Bridge alternately switches the DC bus polarity across the load, producing a high-frequency SPWM waveform.

---

# EGS002 SPWM Controller

The H-Bridge is controlled using the **EGS002 Module**, which integrates:

- EG8010 Pure Sine Wave Generator
- Gate Driver Circuit
- Dead Time Control
- SPWM Generation
- Protection Functions

Advantages:

- High-quality SPWM waveform
- Stable 50 Hz output
- Reduced Total Harmonic Distortion (THD)
- Reliable gate driving

The EGS002 directly drives the IRFP460 MOSFETs.

---

# Output LC Filter

The H-Bridge initially produces a high-frequency SPWM waveform.

An **LC Low Pass Filter** removes switching harmonics and reconstructs a smooth sinusoidal waveform.

Benefits:

- Pure sine wave output
- Reduced harmonic distortion
- Lower EMI
- Improved compatibility with sensitive electronic loads

---

# Voltage Feedback

A voltage feedback network continuously monitors the AC output voltage.

Purpose:

- Maintain constant output voltage
- Compensate for load variations
- Improve regulation
- Enhance stability

This feedback ensures a regulated 230 V AC output.

---

# Current Feedback

A current sensing circuit continuously measures output current.

Maximum Output Current:

**Approximately 5 A**

Functions:

- Overcurrent protection
- Short circuit detection
- Prevents MOSFET damage
- Improves reliability

---

# Cooling System

Power MOSFETs dissipate heat during operation.

Forced-air cooling is provided using DC cooling fans mounted on the heatsinks.

An **NTC Thermistor** continuously monitors heatsink temperature.

Automatic fan control:

- Fan ON when temperature exceeds threshold
- Fan OFF after sufficient cooling

This minimizes power consumption and extends fan life.

---

# Protection Circuit

A dedicated protection circuit based on the **LM393 Comparator** provides system safety.

Implemented protections include:

- Input Over Voltage
- Input Under Voltage

The protection thresholds are set using resistor divider networks.

When a fault is detected:

LM393 output drives the **Shutdown (SD) pin** of the SG3525.

This immediately disables PWM generation, protecting the transformer and MOSFETs from damage.

---

# Features

- 1 kW Output Power
- Pure Sine Wave Output
- Transformerless High-Frequency Design
- Push-Pull DC-DC Converter
- Full Bridge SPWM Inverter
- SG3525 PWM Controller
- EGS002 SPWM Generator
- IRFP460 MOSFET H-Bridge
- High Frequency Ferrite Transformer
- Temperature Controlled Cooling
- Automatic Fan Control
- Voltage Feedback Regulation
- Current Feedback Protection
- LC Output Filter
- LM393 Protection Circuit
- High Efficiency
- Compact Design

# Hardware Used

## Controllers

- SG3525 PWM Controller
- EGS002 SPWM Generator

## Power Devices

- IRFP460 MOSFETs

## Protection

- LM393 Comparator

## Passive Components

- 470 µF Electrolytic Capacitors
- 100 nF Film Capacitors
- LC Output Filter
- NTC Thermistor

# Future Improvements
- Modular Design
- Digital voltage regulation using a microcontroller
- LCD-based monitoring interface
- Wi-Fi/IoT monitoring
- Battery State-of-Charge estimation
- Remote fault diagnostics
- Efficiency optimization
- Closed-loop DC bus voltage control







 
