# 4 Parts

A sequencer app for Ornaments + Crimes that emulates composing four-part harmony.

[<img src="https://github.com/jddinneen/4parts/blob/main/4parts.jpg" width="50%"/>](https://github.com/jddinneen/4parts/blob/main/4parts.jpg)

## Description and user guide

**4 Parts** is a 4-channel, 99-step sequencer app for Ornaments & Crimes (O_C) that emulates composing four-part harmony on sheet music. Four chords/steps are displayed at a time across two staffs: the active step, which is highlighted to show it is editable and determines the current output, the step before, and two steps after. Each chord has four notes, one per output, with its own icon: a hollow circle and square for A & B and a filled versions for C & D (an on-screen legend keeps this clear). Long press down toggles between the staffs and settings screens, long press right encoder does the usual (menu/save). Settings include root(/tonic) and scale(/mode), channel octaves, and looping start and end points. Accidental notes (e.g. sharps) of the tonic/mode combination are not yet visually indicated, but function correctly nonetheless. All 99 chords are saved on command, loaded on boot, and can be cleared in the usual O_C way.

**Composing & playback**: on the staff screen you set the active step's notes, where the left knob moves (up or down) the notes for channels A/B (short press to toggle), and the right knob for channels C/D. The output and icon that each knob is currently editing is shown on the bottom right (1-4 rather than A-D to avoid confusion). All 99 steps/slots can be navigated manually, e.g. during composition, using the down (forward) and up (backward) buttons (incl. wrapping from 0 to 99 and vice versa) or by choosing the active step in the settings menu. Although playback can be achieved manually with the navigation controls, the digital inputs (TR1-4) move similarly backward and forward *within the loop points*, to the loop start point (i.e. reset), and to the loop end, respectively. CV1 sets the active step so that you can (e.g.) jump to random chords or scrub through the song with a macro controller; CV2 does the same but only within the loop. You can also choose the active step from the settings menu. Long pressing the left encoder will either (as configured in the settings menu) (a) go to step zero (i.e. reset) or (b) copy the notes from the current step *or* paste the last copied notes to the current step. Which action will happen is shown via characters on the right: L0, LC(opy), or LP(aste). Just above that, the current step number is displayed.

**Limitations**: setting a single note to be outside the scale (e.g. a C# while in C) is not currently supported, but could be achieved with a precision adder. Note *length* (e.g. half notes, triplets...) is also not handled by the app, but can be achieved with VCAs. Currently only the 7 modern Western modes are present. And most notably, I wrote this app with no prior experience of C++/Arduino, so there are likely bugs, problems, ugly code... I take no responsibility for your use of the app, flashing, wasted time, etc.

**Credit**: see the app's ino file.

## Installing 4 Parts

As with the default O_C firmware there are two possibilities:
 1. [Download](https://github.com/jddinneen/4parts) and flash the pre-compiled hex file, which is the default O_C firmware but with some apps replaced with this one.
 2. [Download](https://github.com/jddinneen/4parts) the app file (APP_FPART.ino) from github, put that file in the O_C firmware compilation folder, add the app to the apps array(s) near the top of OC_APPS.ino (e.g. DECLARE_APP('F','P', "4 Parts", FPART, FPART_isr)) and comment out a few other apps to make space for this one, then compile and flash as normal. *You need at least five apps* enabled, but not so many that all the storage space or dynamic memory is used up (the compiler will warn you).

How to do the compiling and flashing is covered [here](https://ornament-and-cri.me/firmware/).

## Possible additions
 
 - use CV3 and CV4 for something -- maybe change root and mode?
 - might be possible to draw the current scale's signature (sharps, double sharps etc) on left side of staffs.
 - might be possible use the mask specification on top of a scale, causing note icons to skip notes removed from the scale. Implementing this might also enable using the full range of scales built into the O_C.
