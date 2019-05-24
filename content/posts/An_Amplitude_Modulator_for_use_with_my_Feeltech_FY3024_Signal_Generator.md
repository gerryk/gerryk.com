---
title: "An Amplitude Modulator for use with my Feeltech FY3024 Signal Generator"
date: 2017-03-13T13:48:00+01:00
draft: false
---

I recently bought a new signal generator, the Feeltech FY3024. I chose this unit after a good amount of research on various Ham Radio forums, and the ever-useful EEVBlog. The consensus is that of the various Chinese function generators, the FY3024 is the best combination of cost, features and implementation. There are others, but they fall short, often on the quality of output, which is pretty important in a signal generator.

One feature I was looking forward to using is the Amplitude Modulation feature, but when I attempted to use it, I discovered it is basically a static waveform, with a 100KHz carrier modulated by a 1KHz audio frequency signal. Pretty much useless in an RF environment. However, the FY3024 has 2 independent channels, both of which are capable of generating signals from 0 - 24MHz, so I though if I was to build an outboard Amplitude Modulator, I could use one channel as the carrier and the other as the modulation signal, giving me the desired Amplitude Modulated signal at the output.

I used a design I found at this site, which happily used components I had to hand in the parts-box. Some soldering later and I have something to test.

I applied a 1MHz signal to the carrier-in port, and a 1KHz signal to the audio-in port. I connected the output to the scope, terminated with 50ohms to match the AM output impedance.

;

