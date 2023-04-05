# Overview

The drawing below provides an overview of the work to be done for the "Box" (which is what we are calling the Hardware-and-Electrical Box to extend the capabilities of our existing PCB (printed circuit board)

The three sections of the above drawing are described below ( 1 - Existing AC Unit, 2 - Upgrades Needed, 3 - Box Detail)

![scope and conceptual design](img/scope-and-conceptual-design.jpg)


## 1 - Existing AC Unit

Existing system is a one-pipe liquid-based system used for heating and cooling
with a fan that blows the conditioned air into the room. The pipe has a tray to catch
condensate (when in cooling mode).

Today, a branch circuit's wires enter through the back of the AC unit
and feeds a junction box where:

- an electrically powered fan connects to the branch circuit
- two-speed fan wiring connects to OFF/LOW/HIGH toggle switch
- duplex 120V receptacle connects to branch circuit

The ON/LOW/HIGH toggle switch and the duplex receptacle are mounted on AC unit
exterior for the convenience of the tenant to have additional power outlets as well as allowing the tenant to contol the fan speed.

The fan motor is single-phase, permanent split-capacitor with two
speed settings: LOW and HIGH (otherwise, it is OFF). The Fan motor has three wires: common, LOW speed, HIGH speed.

## 2 - Upgrades Needed

For each AC unit that gets upgraded, an electrician will remove the fan switch and replace it with the new relays (that will be in the 'Box'), so now these relays -- and ultimately the fan itself -- can be controlled by the Radiator Labs (RL) panel (Note: the panel is a new user interface provided by RL and is
outside the scope of this work). The new relays you will add to the "Box" will control the existing fan's modes of 
OFF/LOW/HIGH. Relays are mounted inside of new box to be
installed inside of AC unit.

Your box will have a liquid level sensor to the condensate tray to
trigger alarm on *condensate overflow*. You can determine the
sensor type, and here one we have looked at
https://sstsensing.com/product/optomax-digital-range-of-liquid-level-switches-2/.
It is very important to note that water sensor will be 8 feet of
wire away from the box, so the solution for the water sensor must
be tested to work with 8 feet of wire.

The interface between "the Panel" (which is the Radiator Lab's Printed Circuit Board (PCB)) and the new sensor and two relays is an I2C GPIO
expander. RL panel is the I2C master. Therefore, the Box needs to have an I2C GPIO expander.

The Box also provides a single receptacle to power RL Panel, which has an AC adapter.
The AC adapter powers RL panel with 12VDC. The 4-wire connection from the RL
Panel to box is 12VDC power and I2C bus.

The wiring diagram: https://github.com/Radiator-Labs/coop-share/blob/main/README-02-box-build.md#inside-the-box shows outlet for plugging in 12VDC and shows outlet and fan wiring tapping into branch circuit. Part of the your work as a freelancer is to write the instructions for the on-site Electrician to do this work and provide list of materials to purchase for the Electrician. The outlet and fan wiring connections are inside the new box, so the freelancer provides those and installs them in the new boxes. The on-site Electrician connects the branch circuit wiring to the new box following the freelancer's instructions.

## 3 - Box Detail

This is a conceptual sketch. We expect the Box will include
additional materials to be determined by you, such as electrical
wiring termination and electrical protection/safety.

The box contains both 120VAC wiring and low voltage DC wiring
(12VDC / 5VDC / 3.3VDC). The components *inside* the box are:

- A 120v receptacle to power the RL Panel
- I2C GPIO expander to interface between the RL Panel and the water sensor and relays, which control the fan
- voltage regulator to generate the 5VDC / 3.3VDC (required by
  the I2C GPIO expander) from the 12VDC provided by the RL Panel
- two SPDT relays (single pole, double throw relays)

New components installed *outside* the box are:

- liquid sensor

## Deliverables

Final deliverables include:

- 1 Box builds
- Approval of Box Build
- 9 more identical box builds post approval
- bill of materials
- video demonstration of all functionality (fan on/low/high, water sensor detecting, etc.)
- video demonstration of all tests (detailed below in 'scope of work' section)
- instructions for Radiator Labs (RL) to repeat all tests
- installation instructions either in written or video form for:
    - (written) connecting box to existing branch circuit wiring
    - testing fan control using computer-controller I2C master
- CAD drawings:
    - box (dimensioned drawing detailing any modifications)
    - design (layout of parts within box)
    - box-insert-diagram (printed drawing glued inside box)

## Scope of work

Scope of work includes:

- implement the design using off-the-shelf components
    - *custom PCB design is outside the scope of work*
- identify off-the-shelf electronic components (such as
  development boards)
- identify all electrical materials and wiring methods (such as
  conductor type and size, termination methods, method for
  running existing branch circuit wiring into new box, etc.)
- identify requirements, if any, for over-current protection and
  disconnect switch inside the new box
- instructions for on-site electrician to connect your box
- build and test one box and demo to RL for approval prior to
  building all ten boxes
    - perform all tests of functionality on first box build
    - perform smaller set of tests on subsequent builds
- use of test proxies:
    - purchase a [Bus
      Pirate](https://www.sparkfun.com/products/12942) *any
      USB-to-I2C master is acceptable, I refer to it as "Bus
      Pirate" throughout these specifications*
    - Bus Pirate is a test proxy for the RL user interface panel
      (you will not receive an RL panel, but if the box works
      with the Bus Pirate as I2C master, it will work with the RL
      panel as I2C master)
    - find a two-speed, permanent split-capacitor (PSC) fan motor
      to use as a test proxy for the existing fan motor
- write Python scripts to use a Bus Pirate as I2C master
    - RL TODO: we will write the core set of scripts here. We need you, the freelancer, to be comfortable enough with Python to run the script and modify it as needed.
- tests of functionality are driven by the Bus Pirate:
    - Bus Pirate reads liquid sensor
        - liquid sensor trips at 1-inch liquid height
        - liquid sensor does not trip below 1-inch liquid height
    - Bus Pirate controls the two relays
        - opens and closes relay 1
        - opens and closes relay 2
    - Bus Pirate sets fan OFF/LOW/HIGH:
        - connect relays to PSC fan motor
        - demonstrate final system runs fan OFF/LOW/HIGH
- identify, and demonstrate design is in compliance with,
  any applicable articles from [NFPA 70
  (NEC)](https://link.nfpa.org/free-access/publications/70/2023)
  and from NYC Electrical code: [Local Law 39 of
  2011](https://www.nyc.gov/assets/buildings/pdf/ll39of2011_electrical_code.pdf)
    - The design must be safe to install/maintain and must not
      pose a fire hazard.
    - *Sign off by a professional engineer (PE) is outside the
      scope of work.*

## Milestones

We will work together to determine the final milestones. The following list of milestones are
a starting point for the discussion:

- M1: Select parts and submit to RL for approval
- M2: Submit CAD design drawing of box to RL for approval
- M3: Build one box and submit video demo of functionality for
  approval
- M4: Perform tests and submit video of test activities and
  results to RL for approval
- M5: Submit updated CAD design drawings to RL with final
  information and all detail necessary to fabricate the design,
  to operate the box, and to run all tests
- M6: Ship first box to RL for final approval
- M7:  proceed with builds of remaining 9 boxes, test 9 boxes and ship to RL

[Back to README.md](README.md)

