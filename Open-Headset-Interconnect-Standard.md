# 1. Open Headset Interconnect Standard

* Open: Any individual or company may make devices compliant with this standard, with no obligation.
* Headset: Describes the signaling commonly found between a user and a radio: Microphone, Headphones, and Push To Talk.
* Interconnect: Describes both the physical and electrical connection of those signals between the user and radio.
* Standard: Devices built to this standard will work with other devices built to the same standard.

There are so many different connections for microphone, headphone, and PTT that it is improbable you can take your preferred headset and connect it to any radio without a conversion device, and adapter, in between.  Before OHIS, you'd need a full-mesh of adapters to go from every headset type to every radio type: O(N^2) adapters.  By defining OHIS, one can now build or purchase only one adapter for each device for full interoperability: O(N) adapters.

**TODO** Real world example?

- [1. Open Headset Interconnect Standard](#1-open-headset-interconnect-standard)
    - [1.1. tl,dr: Quick technical definition of standard](#11-tldr-quick-technical-definition-of-standard)
- [2. Why? What problems does this standard address?](#2-why-what-problems-does-this-standard-address)
- [3. Standard Details](#3-standard-details)
    - [3.1. Physical](#31-physical)
    - [3.2. Electrical](#32-electrical)
        - [3.2.1. Microphone](#321-microphone)
        - [3.2.2. Headphone](#322-headphone)
        - [3.2.3. Power](#323-power)
        - [3.2.4. PTT](#324-ptt)
- [4. Acceptable Compromises](#4-acceptable-compromises)
- [5. Contact and Contribution to the OHIS](#5-contact-and-contribution-to-the-ohis)

## 1.1. tl,dr: Quick technical definition of standard

A quick summary of the physical and electrical standard follows. If you have any questions, please see the [Standard Details](#13-standard-details) section below.

![OHIS Overview](Images/OHIS%20Overview-2390x699.png)

There are two participants:

* User: Describes the "headset" side of the interconnect.  Consumes the Headphone signal, generates the Microphone signal, and will trigger Push To Talk (PTT).  Optionally uses the Vcc provided by the Radio side.
* Radio: Describes the device the "headset" connects to.  Generates the Headphone signal, consumes the Microphone and PTT signals, and provides power to Vcc.

OHIS us an 8P8C/RJ-45 connector, using TIA-568B wiring, shielded cable preferred but not required.

| Pin | Direction | Description |
|---|---|---|
| 1 | Radio -> User | Vcc Power.  Typically 5vDC, 200mA. 3.3vDC is acceptable. Fused or current limited. |
| 2 | User -> Radio | Push To Talk. User pulls to Power Ground. Pulled up to no more than 5vDC. |
| 3 | Common | Microphone Ground |
| 4 | Radio -> User | Headphone Left Audio |
| 5 | Common | Headphone Ground |
| 6 | User -> Radio | Microphone audio, Electret (DC bias provided by Radio on this pin) |
| 7 | Common | Power/PTT Ground |
| 8 | Radio -> User | Headphone Right Audio |

**Microphone:** The Microphone signal is a typical Electret microphone signal: 5vDC bias provided by the radio to power the microphone element, via 2.2k ohm resistor.  Dynamic microphone elements will require about 10 to 15db of amplification.  This standard also provides a simple 5 component microphone pre-amp, powered by this 5vDC bias, to bring a Dynamic microphone element up to Electret signal levels.

**Headphones:** The Headphones signals are typical 16 to 64ohm headphones, about 1v RMS at full volume.  If the source is mono, it must drive both Left and Right signals and can just tie them in parallel (assuming the driver can handle the lower impedance.)  If the destination is mono, it can choose to either use only the Left audio, or to mix Left and Right together.

**Power:** The Radio must provide at least 200mA of 5vDC (where possible, but as low as 3.2vDC is acceptable if not), for the User device to run amplifiers, DTMF/tone generators, signal processing, etc.

**PTT:** The User triggers PTT using a simple contact closure to Power Ground.  The Radio side must not pull it up to any higher than Vcc.

**GROUNDS!** Where possible, the User devices will keep the three Grounds separate: 1) Mic and Mic Ground, 2) Headphones Left/Right and Headphone Ground, and 3) Vcc/PTT and Power Ground.  This will allow for the best audio quality, least cross-talk, fewest ground loops, etc.

But in some cases, this isn't possible.  eg: A 4-pin TRRS Headset connector which shares a common ground between the Mic and Headphones.  **THE RADIO DEVICE MUST SUPPORT THIS.**  The Radio MUST NOT require anything other than "Ground" on the Mic or Headphone Ground pins.  That is, no push-pull on the Headphones, no DC bias'd Mic Ground, etc.

# 2. Why? What problems does this standard address?

# 3. Standard Details

## 3.1. Physical


The connector is an 8P8C Modular connector, commonly ([but incorrectly](https://en.wikipedia.org/wiki/Modular_connector#8P8C)) referred to as an RJ-45.  Given that nearly the entire telephony and networking industry has adopted the (technically-incorrect) use of "RJ-45", we will also refer to it as "RJ-45" in this document despite the technically-incorrectness of the term.

The cables used must be wired as TIA-568B.  Specifically, OHIS assumes wires are paired as described in TIA-568B: 1&2, 3&6, 4&5, 7&8.  (TIA-568A also works for straight-through cables (pairs are on the same pins), but when pair colors are discussed in this document we will use TIA-568B colors.)

The above allows the use of common off-the-shelf "Ethernet" cables for use when connecting OHIS devices.  Any category from Cat5 or above will work; OHIS has no high-speed requirements on the cable.

Shielded cables are preferred, but not required.  Either whole-cable shields, like used in Cat5 STP, or per-pair shields, like used in Cat6A and above, will work.  When per-pair shields are used, all shields are terminated together.

## 3.2. Electrical

### 3.2.1. Microphone

### 3.2.2. Headphone

### 3.2.3. Power

### 3.2.4. PTT

# 4. Acceptable Compromises

# 5. Contact and Contribution to the OHIS