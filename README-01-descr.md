# Description

## Existing AC unit

Each existing AC unit consists of:

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

## AC unit upgrade

This diagram shows the relationship between the existing AC
unit, the new box, and the Bus Pirate to the test computer.

The Bus Pirate and computer are a proxy for the new user
interface by RL. *The new user interface is not in the scope of
work.*

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

*The diagram only shows electronics, it does not show any of the
electrical work.*

The upgrade of AC unit adds the following functionality:

- **control** fan over I2C
    - replace manual switch with relays
    - control relays with GPIO expander
- **monitor** condensate tray over I2C
    - add water sensor to condensate tray
    - monitor output of water sensor with GPIO expander

RL will install new user interface (RL panel) on front
of unit:

![render new front](img/render-new-front.png)

Cables from new user interface (RL panel) pass through hole in
front of unit and connect to the Box. 

Cables include:

- 12VDC power extender cable
- I2C cable

RL TODO: provide part numbers and details on these cables

Condensate tray sensor:

![condensate tray sensor](img/condensate-tray-sensor-location.png)

Use an I2C-GPIO expander to provide I2C controls and monitoring.

Use a Bus Pirate as a proxy for the I2C master. *The I2C master
is outside the scope of this work. Demonstrating control with the
Bus Pirate is included in the scope of work.*

Examples of acceptable GPIO expander boards:

- https://www.adafruit.com/product/4132
- https://www.adafruit.com/product/5346

I2C-GPIO expander
    - see thermopile-share/python/mg_pyplot/simple-example.py
    - use Adafruit 


RL TODO: example Bus Pirate script as I2C master using example

[Back to README.md](README.md)
