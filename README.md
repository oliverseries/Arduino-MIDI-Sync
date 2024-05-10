# Arduino MIDI Sync Firmware

## Description

This software allows for generalised and super tight MIDI sync control over vintage drum machines using an off the shelf Arduino or ATMega328P.

It doesn't use any MIDI library as they're too slow to get a really tight sync, nor does it use the digitalWrite() function as that also isn't fast enough for my liking. Instead, it reads serial directly (only the MIDI command byte, which is all that is necessary for clock sync) and bit bashes the output. This technique is how you get the tightest MIDI sync possible on an Arduino.

## Configuration

Pin 5 is defined as the start/stop output and pin 7 is the clock output. If necessary these can be redefined to use the firmware on other microcontrollers, however this would also require rewriting the bit bashing to work on the new pins/ports.

## Usage

1) Get an Arduino and a shield or adapter board of some variety.
2) Upload the `Arduino-MIDI-Sync.ino` firmware to your Arduino.
3) Add an optocoupler circuit for the MIDI input, connect the output to the RX pin of the Arduino.
4) Locate clock and start/stop signal sources on the drum machine's PCB and cut the trace.
5) (Optional) Make transistor buffer circuits for Arduino output pins.
6) Wire the internal clock and start/stop and Arduino clock and start/stop to a DPDT switch that outputs to the signal destination where you cut the traces.

## Notes

The start/stop function works by latching a pin high when the sequence is running and low when it is not. For most drum machines, this is how the start/stop function works internally. 

However, I have seen some drum machines wherein start/stop works by passing a digital signal through a physically latching switch. In this circumstance, this mod can still work by using the start/stop pin from the microcontroller to control and analog switch IC (4016/4066) that passes the digital signal through.
