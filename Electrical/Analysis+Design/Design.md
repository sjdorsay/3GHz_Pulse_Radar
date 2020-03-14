# Initial Architecture

To remove the effects of the reflected and leaked LO signal from the RX path the two phase shifts, related to , and  should be configured to match . To accomplish this a phase shifter is placed in the LO path to match the leakage phase shift. Once reduced to an acceptable level a second phase shifter can be added to the antenna to match the reflected phase shift.

A low pass filter must be added to remove the additional harmonics from the mixing and the leakage of the mixer.


## Path Characteristics

### Minimum Distance

The minimum distance is determined by the minimum detectable time difference between when a pulse is sent and when it is received. The receiver will not be able to distinguish between sent and received pulse if the pulse is returned during the pulse width.





| Pulse Width (ns) | Sampling Rate (MHz) | Minimum Distance (m) |
| --- | --- | --- |
| 10 | 200 | 2.25 |
| 15 | 200 | 3.00 |
| 20 | 200 | 3.75 |
| 25 | 200 | 4.50 |

### Maximum Distance

The maximum distance is determined by the minimum detectable signal. With the design requirement that the minimum detectable signal be -90 dBm the maximum distance can be achieved using the radar range equation.

### Maximum Power

The maximum returned power is achieved when an object is at the minimum detectable distance

## High Level Spectral Growth Analysis

# Architecture

## Oscillator / PLL

### Reference

### Voltage Controlled Oscillator



### Loop Filter



## Vector Modulator

### I/Q Baseband Signaling

AD8132



### Carrier Feedthrough Nulling

## Analog-to-Digital Converter

### Acquisition Range

The signal that is expected at the input of the ADC is an amplified version of the Minimum / Maximum Power. The ADC must have a dynamic range large enough to support the full power range expected at the output of the receiver block.

The following table lists the minimum input power detectable with an ideal ADC and a given voltage reference.

| Bits | Reference (V) | Resolution (mV) | Power (dBm) |
| --- | --- | --- | --- |
| 8 | 1.8 | 7.03 | -33 |
| 10 | 1.8 | 1.76 | -45 |
| 12 | 1.8 | 0.439 | -57 |
| 14 | 1.8 | 0.110 | -69 |

This table ignores any temperature drifting and aging effects that might cause the effective number of bits (ENOB) to be reduced. When the input power is near the LSB each increment has an uncertainty of about 6 dB. This is far too large for our application so to mitigate this the design must ensure that the signal power seen at the ADC input is 10 dB larger than the LSB.

| N | Reference (V) / Bits | Input (mV) | Power (dBm) |  (dB) |
| --- | --- | --- | --- | --- |
| 1 | 1.8 | 0.44 | -57.14 | 6.02 |
| 2 | 12 | 0.88 | -51.12 | 3.52 |
| 3 |   | 1.32 | -47.60 | 2.50 |
| 4 |   | 1.76 | -45.10 | 1.94 |
| 5 |   | 2.20 | -43.16 | 1.58 |
| 6 |   | 2.64 | -41.58 | 1.34 |
| 7 |   | 3.08 | -40.24 | 1.16 |
| 8 |   | 3.52 | -39.08 | 1.02 |
| 9 |   | 3.96 | -38.06 | 0.92 |
| 10 |   | 4.39 | -37.14 | 0.83 |







| Bits | Reference (V) |  (dB) | Minimum Input Power (dBm) |
| --- | --- | --- | --- |
| 8 | 1.8 | 0.5 | -8 |
| 10 | 1.8 | 0.5 | -20 |
| 12 | 1.8 | 0.5 | -32 |
| 14 | 1.8 | 0.5 | -44 |

This table shows that to have an input power measurement uncertainty less than 0.5 dB the input power must be greater than the calculated minimum power. Since the expected dynamic range is -65 dBm – (-90 dBm) = 25 dB and given that most devices saturate somewhere at or near 0 dBm the only options available to us is to use 12 bit or 14 bit ADC.

### Sampling Rate

In order to achieve a range resolution of less than 5 m using the pulse radar technique the pulse generated must be lower than 30 ns. This pulse width can be considered as the half-period of a periodic modulation meaning that the fundamental frequency is approximately 16.7 MHz.

The Nyquist criteria dictates that the sampling rate must be twice as large as the highest frequency content. Since the pulse is rectangular the spectrum will contain only odd harmonics. To preserve the first three harmonics a filter would have to be designed at 100 MHz which places the minimum sampling rate at 200 MSps.

In order to reduce the range resolution to 2 m the sampling rate needs to be increased to 500 MSps and the cutoff frequency of the filter will need to be increased to 250 MHz.

Therefore the sampling rate needs to be 200 – 500 MSps.

## Antenna Array

## Power Divider



# Link Budget Analysis











# Fault Analysis
