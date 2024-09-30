---
title : "Pixel Art"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---
#### Pixel
**Pixels** are squares, individual dots, of color that are arranged on an up-down, left-right grid.

We can imagine an image as a map of bits, where zeros represent black and ones represent white.

![pixel art](https://raw.githubusercontent.com/baobaoupcloud/cs-w4/main/static/images/1.pixel/pixel1.png)

*RGB*, or *red, green, blue*, are numbers that represent the amount of each of these colors. In Adobe Photoshop, we can see these settings as follows:

![color picker](https://raw.githubusercontent.com/baobaoupcloud/cs-w4/main/static/images/1.pixel/pixel2.png)

Notice how the amount of red, blue, and green changes the color selected.

We can see by the image above that color is not just represented in three values. At the bottom of the window, there is a special value made up of numbers and characters. `255` is represented as `FF`, a hexadecimal.

#### Hexadecimal

***Hexadecimal*** is a system of counting that has 16 counting values. They are as follows:

`0 1 2 3 4 5 6 7 8 9 a b c d e f`

Notice that `a` represents `10` and so on, `f` represents `15`.

Hexadecimal is also known as *base-16*.

When counting in hexadecimal, each column is a power of 16.

- The number `0` is represented as `00`.
- The number `1` is represented as `01`.
- The number `10` is represented as `0A`.
- The number `11` is represented as `0B`.
- The number `15` is represented as `0F`.
- The number `16` is represented as `10`.
- The number `255` is represented as `FF`, because 16 x 15 (or `F`) is 240. Add 15 more to make 255. This is the highest number we can count using a two-digit hexadecimal system.

Hexadecimal is useful because it can be represented using fewer digits. It allows us to represent information more succinctly.