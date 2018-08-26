---
title: Creating an Ultrasonic Microphone
date: 2018-06-17T17:11:45-04:00
draft: false
---

## Introduction

Dodotronics is one of the few reputable microphone brands that focuses on Bat recordings for research. As niche as the company's expertise sounds, there are currently no direct competitor that can deliver the quality and the price point Dodotronics's Mini microphone can offer. Without any alternatives, I have decided to create my own ultrasonic microphone that covers the sensitivities of 50kHz to 80kHz that can compete against **Dodotronic's Mini** **Microphone**. 

## Dodotronic's Mini Microphone

The Dotronics Mini microphone (I will be referring as Mini-Mic) utilizes FG-23629, a MEMS microphone, which is rated between 100Hz to 10kHz. By no means, I cannot say for sure that this microphone module cannot handle frequencies above 10kHz range but without any further sensitivity measurements, it is impossible to know the integrity of the signal without an anechoic chamber with calibrated speakers. In any case above 10kHz, the current Mini-Mic is not acceptable to be used in research settings due to lack of documentation for the ultrasonic frequencies.

Link to the microphone: https://www.digikey.com/product-detail/en/knowles/FG-23629-P16/423-1064-ND/697725

![1531614976487](FG_sensitivty.png)

The Mini-Mic has offered variety of features that is very beneficial in a research setting. The min-mic is one of the smallest microphone that is waterproof, dust-proof, and in some-what readily available form-factor/connector (Weipu). 

![1531615736635](wcasing.png)

![1531616249219](wocasing.png)









## Reversing the Mini-Mic

### Circuit Analysis

One side of Mini-Mic's PCB design was published in the microphone's documentation pages.

![Momimic is composed by two linear  low dropdown voltage regulators and  a double low noise operational  amplifier. The amplification is fixed  and can be changed replacing one or  two resistors.  The standard values are:  RI: 10Kohm  R2: 22Khom  RI regulate the preamplification while  R2 the second amplification  The circuit  RI ](file:///C:/Users/Lucas/AppData/Local/Temp/msohtmlclip1/01/clip_image001.png) 

The microphone module is Knowle's FG-23629 microphone sensor with three leads. 

In this side of the PCB, there are two amplifiers in SOT 23-5 package in non-inverting configuration. With the given fact that R1 is 10Kohm, R2 is 22kOhm, and the input resistors for both amplifiers were 1Kohm, the gain of the amplifiers are 11 and 23 respectively.  

In addition, the signal going from microphone into the first amplifier contains a high-pass filter. The values of the SMD parts were measured to be 1Kohm and 97nF showed that the threshold frequency was roughly 1.6kHz.

On other side, there were three SOT 23-3 packages.  From measuring voltages and the position of pull down resistors, it seems that two SOT 23-3 packages were presumably some kind of MOSFETs/transistors for shutdown functionality as it was daisy changed together to allow 5V to pass into the components.  Lastly, the third SOT 23-3 chip was for 5V to 3.3V step-down voltage regulation. 

Knowing for my purposes, the shutdown capability is unnecessary and I can shave off several components.

### Contents of the Microphone

The bare components needed to constitute a working microphone.

- 2 x Amplifier
- 2 x MOSFET/Transistor
- 1 x 3.3V Voltage Regulator
- 2 x High Pass Filter
- 1 x Microphone Sensor

The internal electric composition of the Mini-Mic is very simple. The new microphone I will be design will be heavily inspired from what I learned through reverse engineering Mini-Mic. 



## Designing the Microphone

All variants of Knowle's FG-23629 are rated between 10Hz to 10kHz so a different microphone sensor needs to be adapted into the design that can fit a wider frequency range. One candidate I was no other than SPU0410LR5H-QB, another sensor from Knowle's.

The frequency sensitivity provided in the SPU0410LR5H's datasheet shows a relative flat best fit line between 40kHz to 80kHz, which is the target frequency for the experiments that will be conducted with this microphone. 

However, I was notified that the microphones sensitivity should be "adequate" enough to listen up to 100kHz.  This statement will be further explored in the testing between this microphone, Dodotronics microphone, and the B&K microphone.

In this post,  FG-23629 will be used to explore and replicate Dodotronic's microphone. Thankfullly, Dodotronics has provided the top side of the PCB for reference.

![dodoschemtatic](dodoschemtatic.png)

It can be clearly with this schematic and cross-referencing the parts that the Dodotronics has two amplifier IC and high pass filters set on them. By using a component meter that I have receieved from China, I was able to decode the resistor and capacitor values.

![dodoschematicwithvalues](dodoschematicwithvalues.PNG)

From the calculations I have done, both amplifiers has the threshold frequency of 1.6kHz, presumably to reduce the signal saturation. From what I gathered, these amplifiers have the slew-rate at least of 2V/uS to be able to accurately amplify a signal of 100kHz.  This value was found by using the equation:

$$
slew\ rate = 2\pi f V \\\\\\
where:f =100kHz, V = 3.3V\\\\\\
2V/\mu s \approx 2\pi f V
$$

Fortunately, the 2V/us was the absolute minimum, and it was easier to find op-amps with higher slew rate. The amplifier that I found suitable was MCP6291T. It is the same SOT 23-3 package as the amplifiers inside the Dodotronics' microphones. 

 	





