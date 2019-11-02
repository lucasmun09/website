---
title: Designing Your Own Ultrasonic Microphone
date: 2019-04-16T17:11:45-04:00
draft: false
---

# Designing Your Own Research Grade Ultrasonic Microphone

Designing a microphone is way harder than it seems. I have only been working with digital electronics as long as I can remember.  I learned the hard way that dealing with analog electronics with small voltages (less than 3.3 V)  is a huge hassle. 

Lower the voltage = easier to be susceptible to noise!

The key take away of this blog post is that I managed to produce a decent microphone with good frequency response on target frequencies (30kHz to 100 kHz). However, I haven't been able to figure out why there is  a sub-hertz signal in my microphone. 

## This Was Done For A Research

In one of my previous posts, I talk about my findings when I tore apart a Dodotronic's microphone. After taking it apart,  I was instructed to make my own microphone design for various reasons:

* Gain control: Old off the shelf microphone does not have gain adjustment
* Form factor:  With the newer soft robotics (bat ears made of silicone) are becoming more complex, we wanted an microphone design that its shape can be quickly adaptive. The older Dodotronic microphones uses WEIPU connectors that most graduate students did not care for.
* Cost: The older microphones cost roughly $150 for each module.  I managed to bring the cost down all the way down to $9 per unit if the PCB was populated by myself or $25 if we outsourced it to the PCB fabrication company.



## Lets Simplify the Circuit!

<hr/>

In one of my previous posts where I reverse engineer the Dodotronics microphone, I learned that the construction of this "ultrasonic" microphone was very simple. 

The microphone simply consisted of a MOSfet to act as a shut down, two amplifiers to amplify the signal, and bunch of supporting passive components that makes the chips work. Finally, the main sensor, Knowles FG sensor's datasheet description indicates that it can be used for hearing aids. 

Over all, I designed my microphone down into three chunks; Sensor, amplification, and power. 



I decided to keep the main sensor the same as the Dodotronics microphone. I did not see any reason not to use the same sensor as its frequency response has been measured and deemed rather "flat".



For amplification, I decided to use (insert name of the amplifier) for the main amplification. I could get the chip in a small SOT-23 package and it only made sense for small microphone application. 



For power, I decided to use an LDO (low drop off) voltage regulator to power the microphone sensor with 2.0 V. The maximum range from the datasheets I have found indicate the sensor can be powered between 1.2 V ~ 2.4 V.  2.0 was arbitrarily chosen because I was able to find them in stock during my designing phase. 



## Circuit Schematic and Layout

What I have effectively designed is a "Bread and Butter" non-inverting opamp that amplifies the MEMs microphone's output. 



// insert schematic here



// The switches you see are jumper pads that you can bridge to allow the use of bandpass filter or bypass it completely.  I should probably move active band pass filtering since I don't know where the source of lower frequency noise is coming form. This will be explained further down in the analysis section.



