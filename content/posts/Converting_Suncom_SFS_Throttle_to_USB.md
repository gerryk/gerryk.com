---
title: "Converting Suncom SFS Throttle to USB"
date: 2015-03-20T13:49:00+01:00
draft: false
---

Having been emboldened by a successful;<a href=http://www.gerryk.com/node/45>conversion of my Thrustmaster F22 Flight Stick</a>, I decided to try to capture all of the buttons on throttle too. A job that worked out easier than I expected as it turned out.

I came across<a href=http://theseger.com/projects/2014/09/converting-suncom-sfs-throttle-usb/>;this page</a>, where a conversion was described. However, this conversion relied on a custom PCB and a SMD PIC which had to be soldered. I have had mixed results in soldering SMD devices with small leg-pitch, so wanted to avoid this route if possible. The author did, however, provide a wiring diagram for the buttons. They are basically wired in a diode-matrix, albeit not on an actual matrix. 3 SELect lines and 8 read lines gives a maximum of 24 buttons. There are actually 18, but since the F22 has 18 already used out of a possible maximum of 32 (DirectPlay controller limitation) we have 14 to play with. Still not terrible.

<img src=https://gerryk.sdf.org/site_images/GripButtonsConnections.png />
(thanks Shai Seger for the drawing)

Since the left and right throttles have their own set of buttons, I doubled up one of the SEL lines on the left with one on the right, and the 4 read lines with 4 from the right also, making sure that there were no overlaps.

<img src=https://gerryk.sdf.org/site_images/2015-03-16%2013.30.36.jpg />

This gave me 11 lines to be brought over to the Teensy in the Joystick. The now unused gameport cable on the throttle has 10 lines, so I would need to use another cable. Once cabled up, I connected the read lines to pins 0 - 7 and the three SEL lines to pins 18, 19&amp;20.

<img src=https://gerryk.sdf.org/site_images/2015-03-16%2014.07.03.jpg />

Once all of this was soldered up, I wrote a small sketch to try to read the buttons. After a number of iterations, and a very informative email from the author of the aforementioned page, I had a working sketch... well almost. It turns out that when a line is brought HIGH or LOW, it takes a very small period of time to happen, so I had to add a very short;<em>delay()</em>;call to provide the necessary time. Incidentally, to read a column, the SEL line must be taken LOW and;<em>digitalRead()</em>;will return 0 for the activated buttons. See the sketch here...

<strong>Throttle-Analyse Sketch</strong>
const int row[8] = { 0,1,2,3,4,5,6,7 };
// 2-dimensional array of column pin numbers:
const int col[3] = { 18,19,20 };
// setup() runs once on boot
void setup() {
;;; Serial.begin(9600);
;;; delay(2000);
;;; Serial.println(SFS Throttle Button analyser);
;;; delay(1000);
;;; for (int x = 0; x &lt; 3; x++) {
;;; ;;; pinMode(col[x], OUTPUT);
;;; }
;;; delay(1000);
;;; for (int x = 0; x &lt; 8; x++) {
;;; ;;; pinMode(row[x], INPUT_PULLUP);
;;; }
}

void loop() {
;;; digitalWrite(col[0], 0);
;;; digitalWrite(col[1], 1);
;;; digitalWrite(col[2], 1);
;;; delay(10);
;;; for (int y = 0; y &lt; 4; y++) { // only 4 buttons on this column
;;; ;;; if (digitalRead(row[y])==0) {
;;;;;;; ;;; Serial.println(y+1);
;;; ;;; };;;;
;;; }
;;; digitalWrite(col[0], 1);
;;; digitalWrite(col[1], 0);
;;; digitalWrite(col[2], 1);
;;; delay(10);
;;; for (int y = 0; y &lt; 8; y++) {
;;; ;;; if (digitalRead(row[y])==0) {
;;; ;;; ;;; Serial.println(y+9);
;;; ;;; }
;;; }
;;; digitalWrite(col[0], 1);
;;; digitalWrite(col[1], 1);
;;; digitalWrite(col[2], 0);
;;; delay(10);
;;; for (int y = 0; y &lt; 8; y++) {
;;; ;;; if (digitalRead(row[y])==0) {
;;;;;;; ;;; Serial.println(y+17);
;;; ;;; }
;;; }
}

Once I had reliable reads, I integrated the code from this sketch into the main F22-SFS sketch, along with proper state-change handling for the buttons. This code can be found here:;<a href=https://github.com/gerryk/USBJoystick/tree/master/f22-sfs>https://github.com/gerryk/USBJoystick/tree/master/f22-sfs</a>

