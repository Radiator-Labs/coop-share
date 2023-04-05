# Overview

The drawing below provides an overview of the work.

![scope and conceptual design](img/scope-and-conceptual-design.jpg)

The three sections of the above drawing are described below.

## 1 - Existing HVAC Unit

Existing system is a pipe with liquid for heating or cooling and
a fan that blows air into the room. The pipe has a tray to catch
condensate (for cooling).

Branch circuit wiring enters through the back of the HVAC unit
and feeds a junction box where:

- fan connects to branch circuit
- two-speed fan wiring connects to OFF/LOW/HIGH toggle switch
- duplex receptacle connects to branch circuit

Toggle switch and duplex receptacle are mounted on HVAC unit
exterior.

Fan motor is single-phase, permanent split-capacitor with two
speed settings: LOW and HIGH.

Fan motor has three wires: common, LOW speed, HIGH speed.

## 2 - Upgrade

Remove fan switch and replace with new relays controlled by Radiator Labs (RL)
panel (the panel is a new user interface provided by RL and is
outside the scope of this work). The new relays you add will control the existing fan's modes of 
OFF/LOW/HIGH. Relays are mounted inside of new box to be
installed inside of HVAC unit.

Remove duplex receptacle and replace with quad receptacle.

Add liquid level sensor to condensate tray to trigger alarm on
*condensate overflow*. The sensor type is to be determined (TBD).

Interface between RL panel and new sensor/relays is an I2C GPIO
expander. RL panel is the I2C master.

Box also provides single receptacle to power RL panel AC adapter.
AC adapter powers RL panel with 12VDC. 4-wire connection from RL
panel to box is 12VDC power and I2C bus.

## 3 - Box Detail

This is a conceptual sketch. We expect the box will include
additional materials to be determined (TBD), such as electrical
wiring termination and electrical protection/safety.

The box contains both 120VAC wiring and low voltage DC wiring
(12VDC / 5VDC / 3.3VDC). The components *inside* the box are:

- I2C GPIO expander
- voltage regulator to generate the 5VDC / 3.3VDC (required by
  the I2C GPIO expander) from the 12VDC provided by the RL panel
- receptacle to power the RL panel
- two SPDT relays

New components installed *outside* the box are:

- liquid sensor (TBD)
- quad receptacle

## Deliverables

Final deliverables include:

- 10 box builds
- bill of materials
- video demonstration of all functionality
- video demonstration of all tests
- instructions for Radiator Labs (RL) to repeat all tests
- installation instructions for:
    - mounting the box
    - connecting to existing branch circuit wiring
    - testing fan control using computer-controller I2C master

Final deliverables may change after discussion.

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
- build and test one box and demo to RL for approval prior to
  building all ten boxes
    - perform all tests of functionality on first box build
    - perform smaller set of tests on subsequent builds
- use test proxies:
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
    - RL TODO: provide sample Bus Pirate script
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

Scope of work may change after discussion.

## Milestones

Split the work up into milestones. We will work together to
determine the milestones. The following list of milestones are
just a starting point for discussion:

- select parts and submit to RL for approval
- submit design drawing of box to RL for approval
- build one box and submit video demo of functionality for
  approval
- perform tests and submit documentation of test methods and
  results to RL for approval
- submit updated design drawings to RL with final information and
  all detail necessary to fabricate the design, to operate the
  box, and to run all tests
- ship first box to RL for final approval
- proceed with builds of remaining boxes
- test boxes and ship to RL

[Back to README.md](README.md)

