---
layout: post
title: Raspberry PI + YwRobot Arduino LCM1602 IIC V1 HD44780 LCD
---

Finally i have some time to write a new post.

Let's start:
I bought a `YwRobot Arduino LCM1602 IIC V1 HD44780 LCD` from Amazon for 6,57 EUR

It has a `I2C` interface (so it will use just 2 cables, `SDA` & `SCL`, + 2 for `VCC` & `GND`).

I found some tutorials online, but they were for Arduino or python... NOTHING FOR C!!
So i decided to write a damn C lib for this component.
I had to cross check various codes/datasheets to understand how it works, but at the end i wrote it.
So, this is my lib! Enjoy it ;)

You can grab from [here](https://github.com/wargio/liblcm1602)

```c
#include <stdio.h>
#include <string.h>
#include "i2c.h"
#include "lcd.h"

#define I2C_FILE_NAME "/dev/i2c-0"

const char* txt[]  = {
    "I work on the PI",
    "via liblcm1602.a"
};

int main(){
    int i2c_dev;
    lcd lcd0;
    // 0x27 is the address of the i2c device
    i2c_dev = open_i2c (I2C_FILE_NAME, 0x27);
    if(i2c_dev <0){
       printf("Error: %d\n", i2c_dev);
       return 1;
    }
    lcd_init(&lcd0, i2c_dev);
    lcd_clear(&lcd0);
    lcd_print(&lcd0, txt[0], strlen(txt[0]), 0);
    lcd_print(&lcd0, txt[1], strlen(txt[1]), 1);
    close_i2c(i2c_dev);
    return 0;
}

```
