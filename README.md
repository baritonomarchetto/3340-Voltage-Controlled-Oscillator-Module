# About This Repository
This repository hosts two versions of my CEM3340 module. Version 2 is the most up-to-date: it's smaller and more in-line with eurorack standards. Version 1 is still here for reference only.

# 3340-Voltage-Controlled-Oscillator-Module
CEM3340 voltage controlled oscillator module for eurorack synthesizers.
The CEM3340 is a legendary voltage-controlled oscillator (VCO) integrated circuit developed by Curtis Electromusic Specialties in the late 1970s. It has been widely used in classic analog synthesizers, including the Sequential Circuits Prophet-5 (starting from Rev.3), Roland Jupiter-6, Roland SH101, Moog Memorymoog and others.

Since 2016, the chip has been reissued, making it available to Companies developing musical instruments, but also to DIY enthusiasts and synth designers (Yaiii! :)).

This "VCO in a package" offers several features that make it a powerful choice for analog synthesizer designs:

- Multiple, independent waveform outputs (sawtooth, triangle, and square/pulse waves)

- Exponential and linear frequency voltage control

- Built-in frequency temperature compensation

- Hard and soft waveform phase sync

- Small footprint

- Great analog sound!

There are plenty of very nice projects and general articles on this IC out there to take inspiration from, but I wanted to build mine keeping some constrains in mind:

- The module had to be as small as possible (I am targeting polyphony)

- Full eurorack compatibility

- Easy to build

- Use of common and cheap components

# Module and Circuit Design
Given the high amount of details Curtis Electromusic put in the [IC datasheet](https://www.bustedgear.com/images/datasheets/CEM3340-3345.pdf), it's not surprising than that most online circuit designs for modules built around the CEM3340 (or it's clones) are heavily based on those found there.

Modifications such as the use of buffers at the (already in-chip buffered) waves out, the normalization of waves amplitudes and some component value adjustment to face supply variations are common (and "due", if you ask me).

The circuit I have layed down here in particular takes inspiration from previous work by [Eddy Bergman](https://www.eddybergman.com/2020/01/synthesizer-build-part-18-really-good.html), which in turn is based on [Digisound's "80"](http://www.digisound80.co.uk/digisound/modules/80-2.htm) design.

For output stages, I took instead inspiration from [Kassutronics](https://kassu2000.blogspot.com/2018/06/vco-3340.html) CEM3340 oscillator module.

The PCB I layed down has all the CEM3340 features made available: frequency control (coarse and fine), three independent waves outs, soft and hard sync inputs, a main control voltage for V/oct input, a secondary, attenuated, linear control voltage input, FM input and pulse wave width control over modulation (PWM).

One point that deserves attention is that CEM3340 outputs positively biased waveforms, but Eurorack standard calls for unbiased oscillators. In [my first iteration of the module](https://www.instructables.com/3340-Voltage-Controlled-Oscillator-Module-for-Modu/) I used decoupling capacitors in series with the outputs (a very common way to decouple audio signals), but this can lead to high pass filtering, to some extent. To keep the wave as "pure" as possible, this time I preferred to play with the output stage and operational amplifiers configuration, in a way similar to how Kassutronics did in his design.

These same output stages are in charge to amplify the waves coming from the IC. Here I cheated the Eurorack standard a little bit, keeping outputs in the 8-9Vpp ballpark instead of 10Vpp (who needs 10Vpp on audio waveform?).

[>>HERE<<](https://www.falstad.com/circuit/circuitjs.html?ctz=CQAgjCAMB0l3BWcMBMcUHYMGZIA4UA2ATmIxAUgpABZsKBTAWjDACgAlcMFcFPEHio8BVGrTjUkVGAjYB3EGgEilKcashsATmvEp1SjLwPiqCQvAUhcGmvrwr7Ua7fDPsad2Z02vYD0InM2Q4VyDvGzw7H0UwDEI9JXwkrUVlJIywSxd0lOyqU3AcrS54xPLwBMiZCT4oBtk2AHMqxMxeSv5RF10u4zbU0KsADxAMJGwIfnJscX1xACEASwBDAGcGABMAHXWAewBXABcABxO99ePV5oY2VaSAh2CQYnAkFiQweHglaEIEAgDAgMDRCHMwYQTP9AShsEJiEDsEDiNgKj80sVhPxwMROjjMRkisTDISBkU3EVMZTDG4nr1BkVKpVhEIrH0cqpWPiet8fr5KkI+AIhVQglY4njhckVATrGApVypaL5crhNUVa1uYJhDxXokZPKcULtSr9g1shaUAgwa9oKQHY6HTQpTB4BBCg1sGxzRUDXwbYlsNBopAwNgyHgSChiGGo1BYHAINMQEG2EA) a Falstad simulation of one of the final stages I used.

With respect to my first module version I left out the attenuation stage for FM input. This way the oscillator module's dimension could stay whithin the 10HP. Not bad for a full-featured, CEM3340 based oscillator module!

An attenuation stage for FM, if necessary, can be easily added with an attenuator [external module](https://www.instructables.com/DIY-Synth-Modules-a-Modular-Approach-Ep1/).

The moudle calls for dual rail supply (+12V and -12V). Suppply voltages are smoothed through capacitors as soon as they hit the module.

The CEM3340 eurorack module is made of three boards: a main board hosting most of the circuits, a front board with potentiometers and in/out jacks, and a panel "plate" board.

The panel board has no traces and should be made out of aluminum alloy, not FR4, for maximum strenght. Boards are intended to be stacked one over each other and are put into electrical comunication through male/female pinheaders.

Components values are directly silkscreened on the PCB, which makes the assembly way easier than consulting a reference sheet.

# How to Tune
A very nice but out-of-tune oscillator is useless. Having it in tune is fundamental to make the best use out of it.

In this Step a simple tuning procedure I drafted, for future reference.

Warning #1: the IC goes into the ultrasound realm with ease. Do not use valued speakers to tune the oscillator or you run the risk to damage them. Use earphones, but do not wear them (your ears are even more valued).

Warning #2: the oscillator output is HOT (8-9Vpp). Use an attenuator before hitting a line mixer desk, or you will likely damage it.

Now that you have been warned about risks, we can start :)

Hardware Needed
For the tuning procedure we are in the need for:

1) a variable voltage source

2) a tuner (software or hardware will do).

A keyboard with CV out will work perfectly as variable voltage source.

Tuning Elements
On the main-board, there are 3 multi-turn trimmers for tuning: trimpot TA, trimpot TB and trimpot TC.

"TC" has only effect at higher frequencies (remember the "high frequency compensation" thing?), so forget it.

"TB" is the trimmer actually affecting tune tracking, so we will concentrate on that one.

There's a jumper on the main board. It's use is to disable the coarse potentiometer during tuning procedure. In it's "normal" position the coarse frequency potentiometer is engaged; on "tune" position corse pot is disabled.

Tuning Procedure
1) Disable coarse pitch control by moving the jumper on the main board from "normal" position to "tune".

2) Set fine pitch control at half-way.

3) Get your output from the SAW wave. If you prefer to use pulse wave, don't forget to put PWM potentiometer at half way or you run the risk to have no output and start thinking something is wrong with your module ;)

4) Turn potentiometer TB fully clockwise. You have now fully compressed your tracking range, so you will hear nothing on the whole keyboard range.

5) Apply a 4V signal (or press C5 on your CV keyboard) to the V/oct input.

6) Turn trimmer TB clockwise untill you hear something. Use the fine pitch potentiometer to find a spot where the wave frequency is detectable by your tuner (or at least audible). Tracking is very sensible, so move TB in small steps. If you have problems finding the spot, go back to point #4 and give TA some counterclock wise turn.

7) Apply a 4V signal (or press C5 on your CV keyboard) to the V/oct input.

8) Tune to the closest note/pitch by rotating the Fine tuning potentiometer. Which note doesn't matter!

9) Apply a 2V signal (or press C3 on your keyboard).

10) If the pitch is higher than two octaves with respect to the previous one, turn TB clockwise by a small amount. If the pitch is lower thatn two octaves, turn TB counterclockwise.

11) Go back to point #7 and repeat untill your scaling is okover the whole octaves range of your interest.

Please notcie that TB is very sensible. Even a small degree turn highly affects tracking.

If after going through the whole procedure the scaling is still not ok, give TA a turn.

When the scaling procedure has ended and your tuning is ok, re-enable the coarse tuning control by moving the jumper back to "normal" position.

# Acknowledgments
Many thanks to the nice girls and guys at [JLCPCB](https://jlcpcb.com/IAT) for sponsoring this module's PCBs. Without their contribution this project would have never reached it's actual level of developent.

JLCPCB is a high-tech manufacturer specialized in the production of high-reliable and cost-effective PCBs. They offer a flexible PCB assembly service with a huge library of more than 600.000 components in stock.

3D printing is part of their portfolio of services so one could create a full finished product, all in one place!

By registering at JLCPCB site via [THIS LINK](https://jlcpcb.com/IAT) (affiliated link) you will receive a series of coupons for your orders. Registering costs nothing, so it could be the right opportunity to give their service a try ;)

My projects are free and for everybody. You are anyway welcome if you want to donate some change to help me cover components costs and push the development of new projects.

[>>HERE<<](https://paypal.me/GuidolinMarco?country.x=IT&locale.x=it_IT) is my paypal donation page, just in case ;)




