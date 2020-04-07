# pdp11code
Short blocks of code for pdp-11 computers.  They are stored as human-readable octal dumps.  I use my `serial11` program to upload them to a running pdp-11 over a serial line.  All of these utilities live below address `010000`, so that's a good place for the `serial11` loader routine.

## utils
A library of useful utilities for various things.

## primes
A light chaser program for the pdp-11/45 that displays prime numbers.

## lfsr
A light chaser program for the pdp-11/45 that displays the contents of a linear feedback shift register.  Set the switches to select bits to be accumulated for feedback.  Uses the line time clock (LTC) interrupt to signal display updates.

## coredump
Another library of useful utilities, this intended for the EMON monitor below.

## emon
An interactive serial monitor.  Load `coredump` first, then this, or load `emon_bundle` which contains everything you need.  Set the stack pointer R6 to `000770`, and then start execution from `001200`.  The monitor expects a DL11 serial console at the usual address `177560`.  

The EMON monitor is set up with five commands:
1. `LIST`, which lists the commands
2. `DUMP`, which sends an octal dump of memory contents over to the serial console
3. `DEPO`, which deposits octal words into memory.  Press ENTER on a blank line to exit.
4. `STRG`, which encodes an EMON standard string (first byte is the string length, followed by byte-packed ASCII characters) in a location you specify from text you type.
5. `VECT`, which starts execution (as a subroutine call) to a specified address.  To get back to the monitor, merely call
```
000207 RTS PC
```
