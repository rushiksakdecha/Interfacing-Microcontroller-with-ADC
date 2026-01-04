# Interfacing-Microcontroller-with-ADC
This project demonstrates the interfacing of an 8051 microcontroller with the ADC0809 (8-bit Analog-to-Digital Converter) to convert analog signals into digital values, which are then displayed on a 7-segment LED display. The firmware is developed using Keil µVision IDE.

The program creates a small lookup table in memory (locations 30H to 3FH). Think of this as a "cheat sheet" — it stores the patterns needed to light up the 7-segment display for every hexadecimal digit from 0 to F. Whenever we need to show a number, we simply look it up from this table.
The program gives friendly names to all the important ADC control pins — things like ALE, START, EOC, and OE — which are all wired through Port-2. The channel selection lines (A, B, C) that pick which analog input to read are also on Port-2. Meanwhile, Port-1 is set up as an input port because that's where we'll receive the digital data from the ADC.
To avoid any unexpected behaviour, the program starts by clearing all the ADC control signals and channel selection bits. It's like resetting everything to a known "off" state before we begin.
Start the Conversion: The program sends a quick pulse on the ALE and START pins (high, then low). This tells the ADC: "Hey, lock in the channel address and start converting!"
Wait Patiently: The ADC takes a tiny bit of time to do its job. The program watches the EOC (End of Conversion) pin, waiting for it to go high and then low again. That's the ADC's way of saying: "I'm done!"
Read the Result: Once the conversion is complete, the program turns on the OE (Output Enable) pin, reads the 8-bit digital value from Port-1 into the accumulator, and then turns OE back off.
