---
title: LCD Problem (two line of boxes) with Anet A8 3D Printer
date: 2018-06-17T17:11:45-04:00
draft: false
---

This was originally posted on Wordpress.com. This post was migrated on 2/3/2019

{{< figure src="lcdwithtwolines.jpg" title="Welcome" height=".25">}}

Two line of boxes are shown in the 2004A LCD.

Do you have this problem and don't want to read it over? Check if your pin 5 or the r/w pin is connected to ground. Also, check your little potentiometer at the back to see if your LCD contrast isn't too high.

Down the rabbit hole we go.

My friend Razi bought an identical 3D printer that I have bought from a different vendor. After helping out building his 3D printer kit for over a course of 6 hours, we found out that his LCD panel wasn't showing the menu. Instead, it was showing two lines filled with boxes which I initially assumed that the LCD was faulty. Without thinking, silly me, I desoldered the LCD module from the PCB panel and hooked it to my Arduino Nano. I uploaded an example code that was in Arduino IDE and what do you know, it works!

{{< figure src="lcd on breadboard.jpg" title="Welcome" >}}



Now I realized that the problem wasn't the LCD but the PCB board that was holding it.

While examining the board, I noticed that the solder pads were basically ripped out during the process of removing the board. I really didn't worry since the problem was actually caused by the connection between the pins and the solder pads.

After I rewired the LCD by following individual traces, I powered it up using the 3D printed controller and the outcome was depressing.

{{< figure src="lcdwithtwolines.jpg" title="Welcome" >}}

At this point, I was lost so I decided to look around at data sheet. It didn't tell me too much about the problem that I was having. I referred back to the wiring at the Arduino code and compared it to the pinout of the PCB board.

WHAT DO YOU KNOW, ONE PIN WASN'T CONNECTED!!!!!

{{< figure src="solderinglcd.jpg" title="Welcome" >}}

The pin was the R/W, or the Read/Write pin that allowed for the LCD to be "written" for new texts to be displayed. To be frank with you, there wasn't a trace connecting that pin to ground so I guess it was a manufacturing defect.

{{< figure src="lcdpinout.jpg" title="Welcome" >}}

So pin 5, R/W, or the Read/Write pin has to be pulled to ground by the looks of the specifications. After I connected pin 5 to ground, ta-dah, it starts working! 

{{< figure src="workinglcd.jpg" title="Welcome" >}}

I have seen a lot of people online having problems with their LCD not functioning in their 3D printers. The 3D printer I got that was $200 shipped didn't have this problem but my friend's oddly did.

So the life lesson today: Don't rip out anything initially. Check pins if they are connected correctly. Check solder pads if they are correctly connected. If your life gives boxes of two lines in your LCD, make sure you connect pin 5 to ground.