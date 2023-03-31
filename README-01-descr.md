# Description

## Existing HVAC unit

Each existing HVAC unit consists of:

- fan
    - fractional horsepower permanent split capacitor fan motor
    - three wires: common, low-speed, high-speed
- hot/cold pipe
- condensate tray

The fan is manually controlled by the occupant using a
single-pole, triple-throw switch mounted on the outside of the
HVAC unit.

The condensate tray catches pipe condensate during the cooling
season. The water often builds up faster than it evaporates;
water spills out resulting in property damage.

## HVAC unit upgrade

```mermaid
flowchart LR

    subgraph i2cmaster["I2C Master (Bus Pirate)"]
        usb[USB]
        i2c[I2C]
    end
    subgraph box["New Box"]
        i2c_io[I2C IO Expander]
        relays[Two SPDT Relays]
    end
    subgraph hvac_unit[HVAC Unit]
        Fan
        condensate[Condensate Overflow Sensor]
    end

    usb --- pc[Computer]
    condensate --- i2c_io
    Fan --- relays
    relays --- i2c_io
    i2c ==I2C=== i2c_io
```

RL upgrade of HVAC unit adds the following functionality:

- **control** fan over I2C
    - replace manual switch with relays
    - control relays with GPIO expander
- **monitor** condensate tray over I2C
    - add water sensor to condensate tray
    - monitor output of water sensor with GPIO expander

Use an I2C-GPIO expander to provide I2C controls and monitoring.

Use a Bus Pirate as a proxy for the I2C master. *The I2C master
is outside the scope of this work. Demonstrating control with the
Bus Pirate is included in the scope of work.*

TODO: I2C-GPIO expander details
