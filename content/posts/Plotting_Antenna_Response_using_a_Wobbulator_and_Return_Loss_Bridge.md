---
title: "Plotting Antenna Response using a Wobbulator and Return Loss Bridge"
date: 2016-05-13T15:21:00+01:00
draft: false 
---
At the Mayo Amateur Radio Rally a couple of years ago, a NI ham, Tom Herbison, MI0IOU was selling an interesting kit for the Raspberry Pi. It combined an Analogue Devices Clock Generator (AD9850) and an RF power meter (AD8307) to give a programmable sweep generator &amp; detector... commonly known as a Wobbulator. I bought one and had an<a href=https://gerryk.com/node/37>enjoyable afternoon not long afterward building it</a>. It was a relatively easy build, and I got some use out of it tuning some Band Pass Filters I had built for use on multi-station portable ops.



More recently, I came across an interesting addition, a Return-Loss Bridge. This allows characterisation of how much RF is absorbed and reflected by the Device Under Test... ideal for testing antennas. I built the RLB based on a design by Wes Hayward, W7ZOI according to this schematic:



<img height=304 src=https://ogfhpa-ch3301.files.1drv.com/y3mhhcBnn5QQVEPdgUuSyPr_EuKXjWc4ujSfkeSbjGdI8UR_C6Q__N-_beKc7eAjHNDQRTXJb1zTXzNGV_i4uvG9oAoPHyqrnY9FvLzJXysHd9-SYsnyg226Ft-49rpiIbT2RI2hepkSuIMRErOBqJEcw?width=470&amp;height=304&amp;cropmode=none width=470 />



I just built it on a piece of scrap PCB material as a prototyping exercise.



<img height=564 src=https://ogh8ba-ch3301.files.1drv.com/y3mhmdCE4vbcyZxiWIILRIsMxFtprefGugupQs7sdb2OMVjYHDUvgtfqrzwnTLr-iIaTBMyQr_Ysi44X1E06zdgBT1HkGhVSgA4nkG5uU4etLfKgvQfLpNPGtjQl9NG9SFhI4_XtQmHNkPXcXkU8CxBMg?width=660&amp;height=564&amp;cropmode=none width=660 />



<img height=571 src=https://oggx4q-ch3301.files.1drv.com/y3mEGmk_6sc1YsKok8tQqGGcWEomSrlhWLomJl4fFEwYVNgK2JxwgmIe0o5yRDoptYKWbOlmEmwHEglC5kYPqXn_cgAZjnmD05dmVGDhNf6JFc3jKxpJJvR_Pberi942t9rB-WuL8GyaJ7uPg0vGIvCGA?width=660&amp;height=571&amp;cropmode=none width=660 />



In order to accurately characterise the Load Under Test, it is necessary to plot the Open and Short paths first. To do this, first connect the Signal Generator to the Detector and plot the response from 0 to 30MHz in appropriate steps. This was my response plot.


<img height=612 src=https://ogerdw-ch3301.files.1drv.com/y3m0CKoTsIGHrLUCMIzWVh1ImEhYZmKxB3r-ONBDbNb2K8tLV_nrtCkxHVwq_ZTivc8ukqjeGikx-0XfGwc1u17vSSarIYSdPjP7KO1H9rNKK3Gwa-93-C_GPT7w_OpjejcBW5BaPAmmda06cI3zWr9Cw?width=660&amp;height=612&amp;cropmode=none width=660 />



Then I plotted the Open path, giving infinite return loss, as expected.



<img height=622 src=https://oghggw-ch3301.files.1drv.com/y3m9if5SZU8dnpVuVUQimKxKSOW9mOZnSwKhdRu3kKrDnr9RUfpXRC2j7dpLe-hL9xUi4HeUfd03ZUGRcSqAL2IQZD7tlfb8B2kA0629-hdoHXjQ07DewSY5i70hyYEbMd08838eVZcl-CjRrFGNqKiBQ?width=660&amp;height=622&amp;cropmode=none width=660 />



I then connected my antenna to the DUT port on the RLB as follows:



<img height=390 src=https://oggcda-ch3301.files.1drv.com/y3m4E_dIl4Hsff6xiFlzSUSoWPiniIvdLDSAy9XYNATcrkW5i9gYn2ZT2zyI0N3MmNQ7JiKEh1idMFUvuiATMzJLrwEJLH0pdfVnUdmi50LEhFlOCiTGgI2LnL8x5MLCm2moQcvt0mMvA0E0u_zgC8pbg?width=660&amp;height=390&amp;cropmode=none width=660 />



I then re-ran the sweep from 0 – 30MHz, giving this plot.



<img height=610 src=https://oggqmg-ch3301.files.1drv.com/y3mQ3ybyBLqRozh_qCmOofBPRUwz9bG4csxHlbTDfaMLe_P_TwM9KXY7mmsBV1TQfHUhTXhY0JpfS1Vijc6GmnDr8i87YaiMiUpG9XckVPRe6NQL7A1faHgKPdZyavWJlvC7zo3RAkpIUo4GscGyAAweQ?width=660&amp;height=610&amp;cropmode=none width=660 />



From this, we can immediately see that there is a good response curve for many of the amateur bands, particularly 80m, 40m, 20m, 17m and 10m. To calculate actual SWR from these figures we can use the following table:



<img height=547 src=https://ogedgq-ch3301.files.1drv.com/y3mmN_75mLVr_SvLogPKDKL48lEYrnjqUo-bnU5GRU0r1GHFDqJsQnoPjpk4e1NminYmbh0ytb4ZrPORa2Iv_tSPSYw2HLvzc47WeLGT2inAbYGVvfmND4A8qkbRRVfh76-FQMm_-84rI_yphazcQQ3FA?width=300&amp;height=547&amp;cropmode=none width=300 />



So, for example, the difference between the short at 80m and the return loss at the same frequency is about 20dB, which gives us an SWR of around 1.2:1. This includes co-ax loss however, so the actual SWR at the feedpoint will be somewhat higher.

