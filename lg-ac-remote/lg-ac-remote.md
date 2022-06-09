# LG Ac IR Remote AKB73975614

My LG AC Remote went bad due to a battery leak and I have been making do 
with my phone's IR blaster and some IR app.

Here's a log of my efforts to repair the remote and to understand its 
internal state machine and the IR code it spits out at each buttonpress.

Then use all this data in another project to build a clone of the remote
accessible over network (MQTT, etc.).

## Log

### Date 0: Understanding its IR Code

### Date 1 [:TODO: Add Date] Surveying and repairing the damage
Lots of carbon pads on the remote have been corroded and few sub solder mask 
trace corrosion as well. Most of the buttons don't work. This is bad.

### Date 2 [:TODO: Add Date] Physical reverse engineering begins!

I scraped off the solder mask at around a dozen places on the remote [] and exposed the copper bus traces underneath.
Upon shorting these, I found most of the button presses.

I don't think I will touch the SLEEP, and TIMER functions. Those can be 
automated better in code later on.

I just need to find a way to automate these shorts to make the process easier.

### 9th June 2022 The LG remote works, sort of.

Admittedly this happened a week or two ago, but after the last update, I immediately discovered that the physical remote signals the AC properly, but I guess the timing is off enough (due to the battery leak) that the [library that I'm using (IRremote library)](https://github.com/Arduino-IRremote/Arduino-IRremote) doesn't recognise it as LG's IR signals.

So I used the Mi Remote App and my phone's IR blaster (which can control the AC properly as well) and decoded its signals with the IRremote library. Thankfully, they are recognied as LG IR signals.

There are a few problems though. Without the physical remote, linking the physical remote's display's icons to its internal state will be impossible. Also, I have to be mindful of the fact that the Mi Remote App's signals is not a direct match to the physical remote's signals. That's because the Mi Remote neither uses the AC model number nor the Physical Remote's model no. to match a remote from its database of over a thousand remotes. During Mi Remote's first setup it uses multiple binary trees to zero in on a match for your device. And in almost every case there's missing, or extra features on the final matched soft remote. And the final UI leaves a lot wanting.

Anyhoo, the signals from Mi's soft remote are LSB-first. Now I have to find some pattern between them, so I can step through them analytically. I don't want to use a lookup table. Those suck.
