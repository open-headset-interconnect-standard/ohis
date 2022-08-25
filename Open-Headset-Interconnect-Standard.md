# 1. Open Headset Interconnect Standard

* Open: Any individual or company may make devices compliant with this standard, with no obligation.
* Headset: Describes the signaling commonly found between a user and a radio: Microphone, Headphones, and Push To Talk.
* Interconnect: Describes both the physical and electrical connection of those signals between the user and radio.
* Standard: Devices built to this standard will work with other devices built to the same standard.

## 1.1. Introduction

There are so many different connections for microphone, headphone, and PTT that it is improbable you can take your preferred headset and connect it to any radio without a conversion device, and adapter.  In this case, you need a full-mesh of adapters to go from every headset type to every radio type: O(N^2) adapters.

With the Open Headset Interconnect Standard, or OHIS, one can now build/purchase only one adapter for each device for full interoperability: O(N) adapters.

This standard builds on the work done by Tom Tengdin [WB9VXY](https://www.qrz.com/db/WB9VXY), with his [Proposed ARES Standard Headset](http://www.sloecc.org/headsets/proposal_ares_standard_headset.pdf).  This standard is different than his proposal in a few places to make it more generalized, and provides more detail and clarity around several points.

- [1. Open Headset Interconnect Standard](#1-open-headset-interconnect-standard)
    - [1.1. Introduction](#11-introduction)
- [2. TL,DR: Summary Technical Definition of the Standard](#2-tldr-summary-technical-definition-of-the-standard)
- [3. Why? What problems does this standard address?](#3-why-what-problems-does-this-standard-address)
    - [3.1. Device Portability](#31-device-portability)
        - [3.1.1. Existing Standards in Ham Radio](#311-existing-standards-in-ham-radio)
        - [3.1.2. No such standard for the User/Radio interface](#312-no-such-standard-for-the-userradio-interface)
        - [3.1.3. Non-OHIS Adapters](#313-non-ohis-adapters)
        - [3.1.4. OHIS Adapters](#314-ohis-adapters)
    - [3.2. Add-On Device Simplification](#32-add-on-device-simplification)
        - [3.2.1. Foo](#321-foo)
- [4. Standard Details](#4-standard-details)
    - [4.1. Physical](#41-physical)
    - [4.2. Electrical](#42-electrical)
        - [4.2.1. Microphone](#421-microphone)
        - [4.2.2. Headphone](#422-headphone)
        - [4.2.3. Power](#423-power)
        - [4.2.4. PTT](#424-ptt)
- [5. Acceptable Compromises](#5-acceptable-compromises)
- [6. Contact and Contribution to the OHIS](#6-contact-and-contribution-to-the-ohis)

<div class="page" />

# 2. TL,DR: Summary Technical Definition of the Standard

A quick summary of the physical and electrical standard follows. If you have any questions, please see the [Standard Details](#4-standard-details) section below.  Similarly, if there are any disagreements, the [Standard Details](#4-standard-details) section is authoritative.

![OHIS Overview](Images/OHIS%20Overview-2390x699.png)

There are two participants:

* User: Describes the "headset" side of the interconnect.  Consumes the Headphone signal, generates the Microphone signal, and will trigger Push To Talk (PTT).  Optionally uses the Vcc provided by the Radio side.
* Radio: Describes the device the "headset" connects to.  Generates the Headphone signal, consumes the Microphone and PTT signals, and provides power to Vcc.

OHIS us an 8P8C/RJ-45 connector, using TIA-568B wiring, shielded cable preferred but not required.

| Pin | Direction | Description |
|---|---|---|
| 1 | User <-- Radio | Vcc Power.  Typically 5vDC, 200mA. 3.3vDC is acceptable. Fused or current limited. |
| 2 | User --> Radio | Push To Talk. User pulls to Power Ground. Radio may pull-up to no more than Vcc. |
| 3 | Common | Microphone Ground |
| 4 | User <-- Radio | Headphone Left Audio |
| 5 | Common | Headphone Ground |
| 6 | User --> Radio | Microphone audio, Electret (DC bias provided by Radio on this pin) |
| 7 | Common | Power/PTT Ground |
| 8 | User <-- Radio | Headphone Right Audio |

**Microphone:** The Microphone signal is a typical Electret microphone signal: 5vDC bias provided by the radio to power the microphone element, via 2.2k ohm resistor.  Dynamic microphone elements will require about 10 to 15db of amplification.  This standard also provides a simple 5 component microphone pre-amp, powered by this 5vDC bias, to bring a Dynamic microphone element up to Electret signal levels.

**Headphones:** The Headphones signals are typical 16 to 64ohm headphones, about 1v RMS at full volume.  If the source is mono, it must drive both Left and Right signals and can just tie them in parallel (assuming the driver can handle the lower impedance.)  If the destination is mono, it can choose to either use only the Left audio, or to mix Left and Right together.

**Power:** The Radio must provide at least 200mA of 5vDC (where possible, but as low as 3.2vDC is acceptable if not), for the User device to run amplifiers, DTMF/tone generators, signal processing, etc.

**PTT:** The User triggers PTT using a simple contact closure to Power Ground.  The Radio side must not pull it up to any higher than Vcc.

**GROUNDS!** Where possible, the User devices will keep the three Grounds separate: 1) Mic and Mic Ground, 2) Headphones Left/Right and Headphone Ground, and 3) Vcc/PTT and Power Ground.  This will allow for the best audio quality, least cross-talk, fewest ground loops, etc.

But in some cases, this isn't possible.  eg: A 4-pin TRRS Headset connector which shares a common ground between the Mic and Headphones.  **THE RADIO DEVICE MUST SUPPORT THIS.**  The Radio MUST NOT require anything other than "Ground" on the Mic or Headphone Ground pins.  That is, no push-pull on the Headphones, no DC bias'd Mic Ground, etc.

<div class="page" />

# 3. Why? What problems does this standard address?

## 3.1. Device Portability

The Open Headset Interconnect Standard allows a User to take their OHIS compliant Headset/Adapter to any OHIS compliant Radio/Adapter.

### 3.1.1. Existing Standards in Ham Radio

There are several physical and electrical standards used in Amateur Radio, such as:

* Power: 13.8vDC +/- 15%.  Anderson Powerpoles are the ARES standard for delivering this power. (Citation needed.)  Before that, there were several physical connectors: "T blade" commonly used in mobile VHF/UHF radios, "6-pin Molex" (but not really a Molex) connector used on desktop HF radios, etc.  But they all carried the same 13.8vDC power.
* RF: 50ohm unbalanced coax with one of several standard connectors: SO-239/PL-259, Type N, BNC, SMA, etc.  Because of the common electrical standard, the connectors are easy to adapt between.

In each case, there's one electrical standard, and at least one physical standard.  But because of the electrical standard, converting between the physical standards is easy.

### 3.1.2. No such standard for the User/Radio interface

Such a standard doesn't exist between the User and the Radio, for either electrical or physical.  Different electrical options include:

* Microphone: What type of mic element: dynamic, electret, or carbon?  Balanced or unbalanced?  Does it require a DC bias voltage, or will a DC bias voltage burn out the mic element?
* Headphones: Mono or stereo?  Is it really a headphone level, or is it a speaker level?  Ground referenced single ended, or push-pull?  
* Push To Talk: Is it a GPIO style contact closure to ground, or does it key by grounding the Microphone element, passing microphone audio through the PTT switch (common on HTs.)

Physical options include:

* Microphone: 3.5mm TS, XLR, one of several different modular plugs (eg: RJ45, RJ6), or 4-pin/8-pin "round aviation" plugs?  Which of the multiple pin-out options for the modular and 8-pin round connectors?  What other signals are available on the mic connector?
* Headphone: 3.5mm or 1/4"?  TS or TRS?
* PTT: Is it on its own connector, or part of the microphone connector?  If its own, is it 3.5mm, 1/4", RCA?  If 3.5mm or 1/4", is it TS, or TRS and shared with a morse key?

### 3.1.3. Non-OHIS Adapters

Making an adapter to go from one specific User interface not designed for the radio (such as an after-market headset) to one specific Radio is certainly possible. Some such adapters will be completely passive, just wires to change physical connectors.  Others may require active electronics, such as amplifiers, which require power.  But all this is possible.  And in a situation with one User interface and one Radio, is the simplest option.

But if that User takes their preferred interface (their headset) to a different radio, such as an ARES EOC or a club Field Day event, and wants to connect it to a radio with a different electrical and/or physical interface, that user will need a different adapter.

### 3.1.4. OHIS Adapters

The Open Headset Interconnect Standard defines both an electrical and physical standard.  Every User builds or buys an adapter to convert their preferred headset to the OHIS standard, and every Radio owner builds or buys an adapter to convert OHIS to their radio.  The OHIS adapters stay with their devices.  User devices can quickly connect and disconnect from Radio devices without concern for the electrical or physical characteristics.  No adapter unique to the pairing of those two devices, headset and radio, is required.

## 3.2. Add-On Device Simplification

The Open Headset Interconnect Standard allows add-on devices designed to connect between the User and the Radio to be greatly simplified.

### 3.2.1. Foo

<div class="page" />

# 4. Standard Details

## 4.1. Physical

The connector is an 8P8C Modular connector, commonly ([but incorrectly](https://en.wikipedia.org/wiki/Modular_connector#8P8C)) referred to as an RJ-45.  Given that nearly the entire telephony and networking industry has adopted the (technically-incorrect) use of "RJ-45", we will also refer to it as "RJ-45" in this document despite the technically-incorrectness of the term.

The cables used must be wired as TIA-568B.  Specifically, OHIS assumes wires are paired as described in TIA-568B: 1&2, 3&6, 4&5, 7&8.  (TIA-568A also works for straight-through cables (pairs are on the same pins), but when pair colors are discussed in this document we will use TIA-568B colors.)

The above allows the use of common off-the-shelf "Ethernet" cables for use when connecting OHIS devices.  Any category from Cat5 or above will work; OHIS has no high-speed requirements on the cable.

Shielded cables are preferred, but not required.  Either whole-cable shields, like used in Cat5 STP, or per-pair shields, like used in Cat6A and above, will work.  When per-pair shields are used, all shields are terminated together.

## 4.2. Electrical

### 4.2.1. Microphone

### 4.2.2. Headphone

### 4.2.3. Power

### 4.2.4. PTT

<div class="page" />

# 5. Acceptable Compromises

<div class="page" />

# 6. Contact and Contribution to the OHIS
