# LG Ac IR Remote AKB73975614

My LG AC Remote went bad due to a battery leak and I have been making do 
with my phone's IR blaster and some IR app.

Here's a log of my efforts to repair the remote and to understand its 
internal state machine and the IR code it spits out at each buttonpress.

Then use all this data in another project to build a clone of the remote
accessible over network (MQTT, etc.).

# Log

# Date 0: Understanding its IR Code

# Date 1 [:TODO: Add Date] Surveying and repairing the damage
Lots of carbon pads on the remote have been corroded and few sub solder mask 
trace corrosion as well. Most of the buttons don't work. This is bad.

# Date 2 [:TODO: Add Date] Physical reverse engineering begins!

I scraped off the solder mask at around a dozen places on the remote and exposed the copper bus traces underneath.
Upon shorting these, I found most of the button presses.

I don't think I will touch the SLEEP, and TIMER functions. Those can be 
automated better in code later on.

I just need to find a way to automate these shorts to make the process easier.
