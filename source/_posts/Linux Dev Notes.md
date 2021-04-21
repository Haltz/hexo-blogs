---
title: 一蓑烟雨任平生
date: 2021-3-31 12:00:00
categories: 随笔
tags: 人生
---

- **bitmap_get_value8**

  这里并不总是能得到8bit，因为取值是按照sizeof(unsigned long)来取，如果想去64n+(56-63)位的值，那么只能取到64n+(7-0)位。

- **bitmap_clear/set**

  这里有个例子，使用bitmap_get_value8(map, start)得到0xff，如果bitmap_clear(map, start, 1)理应得到0x7f，实际上我们得到的0xfe。其实执行是没有错误的，只是这里需要区分大端（Bit 7.6.5.4.3.2.1.0在内存里也是7.6.5.4.3.2.1.0）小端（Bit 7.6.5.4.3.2.1.0在内存里也是0.1.2.3.4.5.6.7）。如果是小端（大部分PC），那么就会有0x7F的情况。因此，**bitmap_clear/set仅仅适用于需要具体到硬件如何存储bit的情况（个人理解），一般情况还是bitmap_set_value8**。

- 

