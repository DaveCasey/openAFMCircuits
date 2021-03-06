# openAFMCircuits

This is the repo for the circuit schematics and layouts for the openAFM board.  Each board is developed on a separate branch.  Current convention is that when the boards are complete and have been manufactured, they are merged with the main branch.  i.e. the main branch should always reflect the current state of the physical boards.

Each board is in a separate subfolder.  Some folders contain text files with "simulation" or "falstadsimulation" or something similar in the name.  These are schematics for a simulation (typically of some part of the circuit).  They can be viewed by going to http://www.falstad.com/circuit/circuitjs.html and importing the text via `File -> Import From Text`.

There are 4 boards that control the openAFM hardware.  These are

1. Main Board
2. Piezo Board
3. Voice Coil Board
4. Input Board

A brief descripion of each board is given below.  For more details look in the folder for each board.  Each board has a pair of 10-pin headers on either side.  These have a female connector on the top, and long lines that extend through the board and produte from the bottom.  These interboard headers allow the boards to stack on top of eachother, whilst sharing 20 common pins.

## Main Board

This board takes in 12V DC from the power supply.  It is responsible for regulating this down to 5V, and distributing power (12V, 5V and GND) to the other boards via the interboard headers.  It is responsible for generating a constant current for the laser diode in the DVD head, and routing signals from other boards (via the interboard headers) to the DVD head.  The DVD head connects directly to this board via a ribbon cable.  The board takes signals from the arduino (via the 10-pin female header) and routes them to the appropriate pins on the interboard headers to be shared with the other boards.

## Input Board

This board deals with the inputs from the 4 photodiode quadrants on the DVD head (labelled as A, B, C and D).  It routes these directly to an ADC, calculates differences and summs in hardware and routes these to another ADC.

## Piezo Board

This board has a 4 channel DAC which is used to control the signals to move each of the 4 piezo quadrants that control the stage movement.  It takes the 4 voltages from the DAC and amplifies them to give a larger range.

## Voice Coil Board

Has a DAC that, along with a pair of push-pull amplifiers, generates the required current to drive the voice coils in the DVD head (focus and tracking).


# I2C Addresses

Here are the I2C addresses of all ICs connected to the I2C bus.

**Part**  | AD5252BRUZ100 | AD5252BRUZ100 | AD5593RBRUZ | AD5696RARUZ | AD5696RARUZ
----------|---------------|---------------|-------------|-------------|------------
**Address (bin)** | 0101111 | 0101100 | 0010001 | 0001100 | 0001111
**Address (hex)** | 2F | 2C | 11 | C | F
**Address (dec)** | 47 | 44 | 17 | 12 | 15
**How?** | AD0 & AD1 to 5V | AD0 & AD1 grounded | A0 to 5V | A0 & A1 grounded | A0 & A1 to 5V
**Description** | Gain Dual digital pot | Gain Dual digital pot | Input ADC | Piezo DAC | Voice Coil DAC
**Board** | Input | Input | Input | Piezo | Voice Coil
**Board Label** | U2 | U6 | U3 | ? | ?
