---
title: "Signal Generator using Adafruit SI5351 Clock Generator"
date: 2015-01-04T13:38:00+01:00
draft: false
---
34,The DDS and related clock generation circuitry has made possible high accuracy, broad-banded programmable VFO functionality for very little money.;<a href=http://www.analog.com/en/rfif-components/direct-digital-synthesis-dds/ad9850/products/product.html>Analogue Devices' AD9850</a>;series offer HF frequencies for about;€5. Higher frequencies can be had for not much more money, with the Silicon Labs SI570 with its near GHz maximum frequency offering the highest. I recently came across;<a href=https://learn.adafruit.com/adafruit-si5351-clock-generator-breakout/overview>an interesting little device from Adafruit. Again, from Silicon Labs, the SI5351</a>;offers 3 independent clock outputs from a single 25MHz reference, programmable via i2c, a maximum frequency of 160MHz and all for less than;€10 shipped. I had to have one.
\nThe order, along with some of the other wonderful goodies from Adafruit arrived soon enough, and I got to work, first off getting the encoder knob working. The plan was to have a rotary encoder with push button for setting the freqeuncy, an i2c LCD for display, and the clockgen, all hanging off an Arduino... in this case, a Leonardo clone.
\n
\n<img src=https://gerryk.sdf.org/site_images/2015-01-03%2023.57.11.jpg />
\n
\nThe sample code I first tried for the encoder worked ok, but then I found the builtin 'encoder' library, and tried that... far better, and no messing with interrupts.
\n
\nNext, I tried to get the display working... no joy using the standard LiquidCrystal_I2C library. I then ran an i2c scanner to find out if the device perhaps had a different address from standard. This gave me a 'no devices' error... something was wrong. After a bit more research, I discovered that the pins used for i2c on the Leo' are not the same as on the Uno.;<em>The Uno uses Analog pins 5 and 6 , whereas the Leo' uses Digital pins 2 and 3</em>. I reran the scanner, and it immediately detected the display on 0x27 ;and the clock-gen on 0x60. I plugged the address into some display testing code and had my display!
\n<img alt=Signal Generator Schematic src=https://gerryk.sdf.org/site_images/signal_gen.png title=Signal Generator Schematic />
\n
\nI then added in a few lines to include the Adafruit si5351 library and program one of the clocks to output 14Hz. I had my AOR8200 MkIII to hand, tuned to 14MHz AM so I hoped to be able to hear the clock on the AOR receiver. Nothing, however. A bit more reading, and I came across;<a href=https://github.com/etherkit/Si5351Arduino>another library for the SI5351</a>... this one managing to avoid all the divider/multiplier calculations necessary with the Adafruit library. I modified the code once again to include this, and instead of doing any calculations, just wrote the required frequency directly to the clock. This time, I could hear a tone on the receiver. As I turned the encoder, the frequency on the display changed, and I could hear the tone get slightly higher in pitch... success by any measure.
\n
\nIt only remains to case this and use it to align a few projects.
\n
\n;
\n
\n<table>
\n\t<tbody>
\n\t\t<tr>
\n\t\t\t<td id=LC1>;</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=2 id=L2>;</td>
\n\t\t\t<td id=LC2>#include &lt;Wire.h&gt;
\n\t\t\t#include &lt;LiquidCrystal_I2C.h&gt;</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=3 id=L3>;</td>
\n\t\t\t<td id=LC3>#include &lt;Encoder.h&gt;</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=4 id=L4>;</td>
\n\t\t\t<td id=LC4>#include si5351.h</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=5 id=L5>;</td>
\n\t\t\t<td id=LC5>;</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=6 id=L6>;</td>
\n\t\t\t<td id=LC6>Si5351 clockgen;</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=7 id=L7>;</td>
\n\t\t\t<td id=LC7>;</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=8 id=L8>;</td>
\n\t\t\t<td id=LC8>const int BUTTON = 8;</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=9 id=L9>;</td>
\n\t\t\t<td id=LC9>long oldPosition = -999;</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=10 id=L10>;</td>
\n\t\t\t<td id=LC10>long int step = 1;</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=11 id=L11>;</td>
\n\t\t\t<td id=LC11>long int frequency = 14000000;</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=12 id=L12>;</td>
\n\t\t\t<td id=LC12>;</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=13 id=L13>;</td>
\n\t\t\t<td id=LC13>Encoder myEnc(5, 6);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=14 id=L14>;</td>
\n\t\t\t<td id=LC14>LiquidCrystal_I2C lcd(0x27,20,4); //set the LCD address to 0x27 for a 16 chars and 2 line display</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=15 id=L15>;</td>
\n\t\t\t<td id=LC15>;</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=16 id=L16>;</td>
\n\t\t\t<td id=LC16>void setup () {</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=17 id=L17>;</td>
\n\t\t\t<td id=LC17>lcd.init();</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=18 id=L18>;</td>
\n\t\t\t<td id=LC18>lcd.backlight();</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=19 id=L19>;</td>
\n\t\t\t<td id=LC19>lcd.setCursor(0, 0);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=20 id=L20>;</td>
\n\t\t\t<td id=LC20>lcd.print(Initialising...);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=21 id=L21>;</td>
\n\t\t\t<td id=LC21>clockgen.init(SI5351_CRYSTAL_LOAD_8PF);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=22 id=L22>;</td>
\n\t\t\t<td id=LC22>lcd.setCursor(0, 1);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=23 id=L23>;</td>
\n\t\t\t<td id=LC23>lcd.print(OK!);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=24 id=L24>;</td>
\n\t\t\t<td id=LC24>delay (2000);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=25 id=L25>;</td>
\n\t\t\t<td id=LC25>pinMode (BUTTON, INPUT);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=26 id=L26>;</td>
\n\t\t\t<td id=LC26>digitalWrite (BUTTON, HIGH); // Pull High Restance</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=27 id=L27>;</td>
\n\t\t\t<td id=LC27>lcd.init();</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=28 id=L28>;</td>
\n\t\t\t<td id=LC28>lcd.backlight();</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=29 id=L29>;</td>
\n\t\t\t<td id=LC29>lcd.setCursor(0, 0);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=30 id=L30>;</td>
\n\t\t\t<td id=LC30>lcd.print(Freq: );</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=31 id=L31>;</td>
\n\t\t\t<td id=LC31>lcd.setCursor(6, 0);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=32 id=L32>;</td>
\n\t\t\t<td id=LC32>lcd.print(frequency);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=33 id=L33>;</td>
\n\t\t\t<td id=LC33>lcd.setCursor(0, 1);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=34 id=L34>;</td>
\n\t\t\t<td id=LC34>lcd.print(Step: );</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=35 id=L35>;</td>
\n\t\t\t<td id=LC35>lcd.setCursor(6, 1);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=36 id=L36>;</td>
\n\t\t\t<td id=LC36>lcd.print(step);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=37 id=L37>;</td>
\n\t\t\t<td id=LC37>// Set CLK0 to output 14 MHz with a fixed PLL frequency</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=38 id=L38>;</td>
\n\t\t\t<td id=LC38>clockgen.set_pll(SI5351_PLL_FIXED, SI5351_PLLA);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=39 id=L39>;</td>
\n\t\t\t<td id=LC39>clockgen.set_freq(frequency, SI5351_PLL_FIXED, SI5351_CLK0);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=40 id=L40>;</td>
\n\t\t\t<td id=LC40>}</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=41 id=L41>;</td>
\n\t\t\t<td id=LC41>;</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=42 id=L42>;</td>
\n\t\t\t<td id=LC42>void loop () {</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=43 id=L43>;</td>
\n\t\t\t<td id=LC43>int delta;</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=44 id=L44>;</td>
\n\t\t\t<td id=LC44>if (!(digitalRead(BUTTON))) {</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=45 id=L45>;</td>
\n\t\t\t<td id=LC45>if (step &gt;= 1000000)</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=46 id=L46>;</td>
\n\t\t\t<td id=LC46>step = 1;</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=47 id=L47>;</td>
\n\t\t\t<td id=LC47>else step = step * 10;</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=48 id=L48>;</td>
\n\t\t\t<td id=LC48>lcd.setCursor(6, 1);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=49 id=L49>;</td>
\n\t\t\t<td id=LC49>lcd.print(step);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=50 id=L50>;</td>
\n\t\t\t<td id=LC50>lcd.setCursor(6+(step/10),1);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=51 id=L51>;</td>
\n\t\t\t<td id=LC51>lcd.print( );</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=52 id=L52>;</td>
\n\t\t\t<td id=LC52>delay (200);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=53 id=L53>;</td>
\n\t\t\t<td id=LC53>}</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=54 id=L54>;</td>
\n\t\t\t<td id=LC54>long newPosition = myEnc.read();</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=55 id=L55>;</td>
\n\t\t\t<td id=LC55>if (newPosition != oldPosition) {</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=56 id=L56>;</td>
\n\t\t\t<td id=LC56>delta = newPosition &gt; oldPosition? 1 : -1;</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=57 id=L57>;</td>
\n\t\t\t<td id=LC57>oldPosition = newPosition;</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=58 id=L58>;</td>
\n\t\t\t<td id=LC58>frequency = frequency + (delta * step);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=59 id=L59>;</td>
\n\t\t\t<td id=LC59>lcd.setCursor(6, 0);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=60 id=L60>;</td>
\n\t\t\t<td id=LC60>lcd.print(frequency);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=61 id=L61>;</td>
\n\t\t\t<td id=LC61>clockgen.set_freq(frequency, SI5351_PLL_FIXED, SI5351_CLK0);</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=62 id=L62>;</td>
\n\t\t\t<td id=LC62>}</td>
\n\t\t</tr>
\n\t\t<tr>
\n\t\t\t<td data-line-number=63 id=L63>;</td>
\n\t\t\t<td id=LC63>}</td>
\n\t\t</tr>
\n\t</tbody>
\n</table>
\n
\n;
\n
\nAn updated version of the code will always be available at;<a href=https://github.com/gerryk/signal_generator>https://github.com/gerryk/signal_generator</a>
\n
