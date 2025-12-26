# 2.4GHz-CMOS-RF-Receiver-Frontend

## Overview

This project presents the design and LTspice simulation of a 2.4 GHz CMOS RF receiver front-end implemented using PTM 180 nm CMOS technology.
The receiver consists of a double-balanced Gilbert cell mixer followed by a single-stage IF amplifier, enabling RF-to-IF down-conversion and gain at low supply voltage.

The design is fully verified using time-domain transient analysis and FFT-based frequency-domain analysis.

## System Architecture

-RF Input Frequency: 2.4 GHz

-Local Oscillator (LO): 2.395 GHz

-Intermediate Frequency (IF): 5 MHz

-Mixer Topology: Double-Balanced Gilbert Cell

-IF Amplifier: Common-Source (CS)

-Supply Voltage: 1.8 V

-Technology: PTM 180 nm CMOS

A high-level block diagram is provided in:

Docs/RF_Receiver_Block_Diagram.png


## Tools & Models Used

-LTspice XVII

-PTM 180 nm CMOS device models

-Transient analysis (.tran)

-FFT-based spectral verification

## Simulation Files

Main schematic used for all results:

LTspice/Gilbert_Mixer_With_IF_Amplifier.asc


## Simulation command:

.tran 0 5u 2u 1p


## Results Overview

The receiver successfully demonstrates:

-Correct RF-to-IF frequency translation

-Differential IF extraction at mixer output

-IF voltage amplification (~20 dB)

-Strong RF and LO suppression at IF

-Stable operation at 1.8 V supply

## Time-Domain Results
1️) Mixer Differential IF Output (Pre-IF Amplifier)

-File:

 Results/Time_Domain/Mixer_Output_Vdiff_Time.png

-Signal:

 V(vdiff) = V(out_p) − V(out_n)

-Observation:

 Clean low-frequency sinusoidal IF envelope

 IF frequency ≈ 5 MHz

 Differential operation suppresses RF and LO feedthrough

 Small amplitude consistent with passive mixer behavior

2️) IF Amplifier Output (Post-Mixer)

-File:

 Results/Time_Domain/IF_Amplifier_Output_Time_Domain.png

-Signal:

 V(IF_OUT)

-Observation:

 IF signal amplified by ~20 dB

 Stable waveform with no distortion

 Proper AC coupling and biasing confirmed

 Demonstrates correct IF stage operation

## Frequency-Domain (FFT) Results
 Mixer Output FFT

-File:

 Results/FFT/FFT_IF_5MHz_Vdiff.png

-FFT Signal Used:

 V(vdiff)

-Observations:

 Dominant spectral peak at 5 MHz

 RF (2.4 GHz) strongly suppressed

 LO (2.395 GHz) strongly suppressed

 Noise floor ≈ 80–100 dB below IF tone

 This confirms correct double-balanced mixing action.

## Detailed Calculations

 All step-by-step calculations are provided in the document:

 Results/Calculations/Mixer_and_IF_Calculations.docx


Includes:

-RF RMS voltage extraction

-IF RMS voltage extraction

-Mixer conversion gain calculation

IF amplifier voltage gain calculation


## Performance Summary Tables

-All consolidated result tables are provided in:

Results/Tables/Performance_Summary_Tables.docx

-Included Tables:

Gilbert Cell Mixer Performance (Pre-IF Amplifier)

FFT-Based IF Verification (Mixer Output)

IF Amplifier Performance Summary

## Key Performance Metrics
Parameter           	Value
RF Frequency	        2.4 GHz
LO Frequency	        2.395 GHz
IF Frequency	        5 MHz
Mixer Conversion Gain	≈ −7 dB
IF Amplifier Gain   	≈ 20 dB
Supply Voltage      	1.8 V
Technology	          PTM 180 nm CMOS


## IF Noise Discussion (Theoretical)

- The Gilbert cell mixer introduces thermal noise primarily from:

   Switching quad transistors

   Tail current source

- Differential architecture significantly reduces:

   Common-mode noise

   Supply-coupled interference

- The IF amplifier noise is dominated by:

   Input transistor channel thermal noise

   Load resistor thermal noise

   Since the IF frequency is only 5 MHz, noise shaping and filtering are effective.
   A full noise figure extraction would require AC noise analysis, which is outside the scope of this transient-based verification.
  

## Linearity Discussion (Theoretical)

-The mixer operates in a current-commutating regime, improving linearity

-Differential structure suppresses even-order distortion

-IF amplifier linearity is limited by:

  Overdrive voltage

  Load resistance

  Bias point

No IIP3 simulation was performed; however, topology and biasing are consistent with moderate linearity suitable for low-IF receivers.


## Future Work

 -Noise figure simulation and extraction

 -Linearity analysis (IIP3, P1dB)

 -IF filter design

 -PLL-based LO generation

 -Layout-aware post-extraction simulation

 -Integration with baseband processing
 

## How to Run the Simulation

Open LTspice XVII

Load:

LTspice/Gil_IFasc.asc

Ensure ptm180nm.lib is correctly linked

Run transient simulation

Observe:

V(vdiff) → mixer IF output

V(IF_OUT) → amplified IF

Use FFT on V(vdiff) to verify 5 MHz IF tone


Author
Udit Bangar
