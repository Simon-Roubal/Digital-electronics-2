# Lab 5: ŠIMON ROUBAL

Link to your `Digital-electronics-2` GitHub repository:

   [https://github.com/Simon-Roubal/Digital-electronics-2/tree/main/Lab_05](https://github.com/Simon-Roubal/Digital-electronics-2/tree/main/Lab_05)


### 7-segment library

1. In your words, describe the difference between Common Cathode and Common Anode 7-segment display.
   * CC SSD - Segments are active on high. All cathodes are linked together.
   * CA SSD - Segments are active on low. All anodes are linked together.

2. Code listing with syntax highlighting of two interrupt service routines (`TIMER0_OVF_vect`, `TIMER0_OVF_vect`) from counter application with at least two digits, ie. values from 00 to 59:

```c
/**********************************************************************
 * Function: Timer/Counter1 overflow interrupt
 * Purpose:  Increment counter value from 00 to 59.
 **********************************************************************/
ISR(TIMER1_OVF_vect)
{
    counter ++;
    if (counter > 9)
    {
        counter = 0;
    }
    SEG_update_shift_regs(counter, 0);
}
```

```c
/**********************************************************************
 * Function: Timer/Counter0 overflow interrupt
 * Purpose:  Display tens and units of a counter at SSD.
 **********************************************************************/
ISR(TIMER0_OVF_vect)
{
    static uint8_t pos = 0;
    
    pos++;
    if(pos > 1)
    {
        pos = 0;
        SEG_update_shift_regs(counter, pos);
    }
}
```

3. Flowchart figure for function `SEG_clk_2us()` which generates one clock period on `SEG_CLK` pin with a duration of 2&nbsp;us. The image can be drawn on a computer or by hand. Use clear descriptions of the individual steps of the algorithms.

   ![obrazek](https://user-images.githubusercontent.com/77580298/138878094-f167ca81-e1dd-4a57-8c38-97c2eeaf4e43.png)


### Kitchen alarm

Consider a kitchen alarm with a 7-segment display, one LED and three push buttons: start, +1 minute, -1 minute. Use the +1/-1 minute buttons to increment/decrement the timer value. After pressing the Start button, the countdown starts. The countdown value is shown on the display in the form of mm.ss (minutes.seconds). At the end of the countdown, the LED will start blinking.

1. Scheme of kitchen alarm; do not forget the supply voltage. The image can be drawn on a computer or by hand. Always name all components and their values.

   ![your figure]()
