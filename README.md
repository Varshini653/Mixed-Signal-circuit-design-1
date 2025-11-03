# Mixed-Signal-circuit-design  
# A Transconductance-Enhanced Latch Comparator for Energy-Efficient High-Speed ADCs
# Abstract
This work introduces a low-power, high-speed dynamic comparator designed for analog-to-digital converter (ADC) applications. The key innovation lies in a transconductance-enhanced latching stage that, unlike conventional cross-coupled inverters, biases all transistors in strong inversion during the reset phase. This approach significantly improves effective transconductance at the beginning of the comparison, resulting in faster regeneration, reduced metastability, and lower energy consumption. Implemented in 180-nm CMOS technology and operating at a 1.2 V supply, the comparator achieves a sampling speed of up to 2 GS/s while consuming only 110 fJ per comparison. Both simulation and measurement results validate its reduced delay, compact area, and superior energy efficiency, making it highly suitable for high-performance, low-voltage ADCs.
# Keywords
Dynamic Comparator, Transconductance Enhancement, Latch Regeneration, Low Power, High Speed, Analog-to-Digital Converter (ADC).
# Introduction
Dynamic comparators are vital in ADCs, high-speed I/O, memory sensing, and BIST circuits due to their fast operation and low static power. Conventional single-stage designs suffer from high voltage headroom requirements and kickback noise. Two-stage topologies with separate preamplifiers offer better low-voltage performance and noise isolation. Prior enhancements have improved speed and power but often increased area or noise. This paper presents a novel two-stage dynamic comparator with a transconductance-enhanced latching stage, achieving faster regeneration and lower energy consumption. Fabricated in 180-nm CMOS, it operates at 1.2 V with 2 GS/s sampling and 110 fJ energy per comparison.
# 1)CONVENTIONAL TWO-STAGE DYNAMIC COMPARATOR
he conventional two-stage dynamic comparator consists of a preamplifier stage and a latching stage. The preamplifier uses low tail current to minimize input offset, while the latch is optimized for high current to boost speed.

Operation Phases:
Reset Phase (CLK = 0): M4 and M5 are ON, charging nodes Dn and Dp to VDD; output nodes OUTp and OUTn discharge to ground.

Comparison Phase (CLK = VDD): M10 and M11 are ON, M4 and M5 are OFF; Dn and Dp discharge based on input voltages (Vinn, Vinp), generating a differential output amplified by the cross-coupled latch.

Advantages:
Lower kickback noise, Better low-voltage compatibility, Flexible trade-off between speed and offset

Delay Analysis:
Total delay tdelay = t0 + t(latch)

t0: Time to build initial output difference; depends on pMOS transconductance

t(latch): Time for output to reach 0.5VDD; depends on combined pMOS and nMOS transconductance

Limitation: 
During t0, only pMOS transistors contribute to transconductance, reducing regeneration speed and increasing metastability and energy consumption.

# Circuit Implementation
<img width="867" height="641" alt="ss2_crop" src="https://github.com/user-attachments/assets/ac1b350b-0bb7-4548-9d0a-50c963b3eada" />

# Specifications

**Parameter	Values**

M0-1 =	2 / 0.18 µm

M2-3 =	1 / 0.18 µm

M4-5 =	0.5 / 0.18 µm

M6-7 =	2 / 0.18 µm

M8-9 =	1.8 / 0.18 µm

M10-11 =	4 / 0.18 µm

M12 	= 0.44 / 0.18 µm

Vdd = 1.2 V

Vinp = 0.6 mV

Vinn = 0.9 mV

clk -> Vpulse -> V1 = 0 V

V2 = 1.2 V

Period = 3 ns
                 

# Working
Two Key Stages:
1. Preamplifier Stage (M1–M6):
M1 & M2: Input transistors receive Vin⁺ and Vin⁻.
M3 & M4: Diode-connected loads convert voltage difference into current.
M5 & M6: Clock-controlled current sources activate the stage during comparison.
Purpose: Amplify small input voltage differences.
2. Latch Stage (M7–M12):
M7 & M8: Cross-coupled inverters regenerate and amplify the signal.
M9 & M10: Switching transistors connect latch to preamplifier when CLK is high.
M11 & M12: Output buffers deliver clean digital results.
Purpose: Make a fast and decisive digital output.

Before CLK is high: Circuit is idle.

When CLK goes high: Preamplifier activates. Latch connects and regenerates signal. Output is generated based on which input is higher.

Proposed Design Enhancements:
Positive feedback in preamplifier → faster regeneration, reduced delay.
Differential latch activation → lower power consumption.
Trade-off: Slightly higher kickback noise, but better speed and efficiency.

# Simulation results
![1](https://github.com/user-attachments/assets/595d2ec0-947d-49f2-bfd2-3610bcc1987d)

In the reset phase, CLK = 0, M4 and M5 are turned ON while M10 and M11 are OFF. Hence, the transistors charge the intermediate nodes Dn and Dp to the supply voltage (VDD). Meanwhile, the output nodes OUTp and OUTn are discharged to ground through M8 and M9. This is important to ensure that the comparator starts each comparison in a clean, defined initial condition.
During the comparison phase, when CLK = VDD, M10 and M11 switch on while M4 and M5 switch off. As a result, the nodes Dn and Dp start to discharge at different rates due to the differential input voltages Vinp and Vinn. Now, assuming that Vinn is fixed at 600 mV, and Vinp is swept during a parametric analysis —

When Vinp < Vinn (600 mV) → the Dp node discharges faster than Dn. The latch amplifies this difference and drives OUTn high and OUTp low.

If Vinp > Vinn (600 mV) → the other way around: Dn discharges faster and OUTp high and OUTn low










