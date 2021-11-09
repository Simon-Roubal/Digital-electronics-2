# Lab 7: ŠIMON ROUBAL

Link to this file in your GitHub repository:

[https://github.com/Simon-Roubal/Digital-electronics-2/blob/main/Lab_07/README.md](https://github.com/Simon-Roubal/Digital-electronics-2/blob/main/Lab_07/README.md)


### Analog-to-Digital Conversion

1. Complete table with voltage divider, calculated, and measured ADC values for all five push buttons.

   | **Push button** | **PC0[A0] voltage** | **ADC value (calculated)** | **ADC value (measured)** |
   | :-: | :-: | :-: | :-: |
   | Right  | 0&nbsp;V | 0   | 0 |
   | Up     | 0.495&nbsp;V | 101 | 100 |
   | Down   |   1.203&nbsp;V    |  246   | 257 |
   | Left   |     1.97&nbsp;V  |   403  | 410 |
   | Select |    3.18&nbsp;V   |   650  | 640 |
   | none   |   5&nbsp;V    |  1023   | 1023 |

2. Code listing of ACD interrupt service routine for sending data to the LCD/UART and identification of the pressed button. Always use syntax highlighting and meaningful comments:

```c
/**********************************************************************
 * Function: ADC complete interrupt
 * Purpose:  Display value on LCD and send it to UART.
 **********************************************************************/
ISR(ADC_vect)
{
    uint16_t value = 0;
    char lcd_string[4] = "0000";

    value = ADC;                  // Copy ADC result to 16-bit variable
    itoa(value, lcd_string, 10);  // Convert decimal value to string

    uart_puts(lcd_string);
    uart_puts("  ");

    lcd_gotoxy(8,0);
    lcd_puts("    ");
    lcd_gotoxy(8,0);
    lcd_puts(lcd_string);
    
    itoa(value, lcd_string, 16);
    
    uart_puts(lcd_string);
    uart_puts("  ");
    
    lcd_gotoxy(13,0);
    lcd_puts("   ");
    lcd_gotoxy(13,0);
    lcd_puts(lcd_string);
    
    if (value>=0 && value<=10)
    {
        lcd_gotoxy(8,1);
        lcd_puts("      ");
        lcd_gotoxy(8,01);
        lcd_puts("Right");
        uart_puts("Right");
        uart_puts("\r\n");
    }
    if (value>=80 && value<=120)
    {
        lcd_gotoxy(8,1);
        lcd_puts("      ");
        lcd_gotoxy(8,01);
        lcd_puts("Up");
        uart_puts("Up");
        uart_puts("\r\n");
    }
    if (value>=220 && value<=280)
    {
        lcd_gotoxy(8,1);
        lcd_puts("      ");
        lcd_gotoxy(8,01);
        lcd_puts("Down");
        uart_puts("Down");
        uart_puts("\r\n");
    }
    if (value>=380 && value<=420)
    {
        lcd_gotoxy(8,1);
        lcd_puts("      ");
        lcd_gotoxy(8,01);
        lcd_puts("Left");
        uart_puts("Left");
        uart_puts("\r\n");
    }
    if (value>=630 && value<=670)
    {
        lcd_gotoxy(8,1);
        lcd_puts("      ");
        lcd_gotoxy(8,01);
        lcd_puts("Select");
        uart_puts("Select");
        uart_puts("\r\n");
    }
    if (value>=1003 && value<=1043)
    {
        lcd_gotoxy(8,1);
        lcd_puts("      ");
        lcd_gotoxy(8,01);
        lcd_puts("None");
        uart_puts("None");
        uart_puts("\r\n");
    }
}
```


### UART communication

1. (Hand-drawn) picture of UART signal when transmitting three character data `De2` in 4800 7O2 mode (7 data bits, odd parity, 2 stop bits, 4800&nbsp;Bd).
![obrazek](https://user-images.githubusercontent.com/77580298/140950991-b1d533e0-10b7-46a6-a595-761391a29f2c.png)

2. Flowchart figure for function `uint8_t get_parity(uint8_t data, uint8_t type)` which calculates a parity bit of input 8-bit `data` according to parameter `type`. The image can be drawn on a computer or by hand. Use clear descriptions of the individual steps of the algorithms.

   ![your figure]()


### Temperature meter

Consider an application for temperature measurement and display. Use temperature sensor [TC1046](http://ww1.microchip.com/downloads/en/DeviceDoc/21496C.pdf), LCD, one LED and a push button. After pressing the button, the temperature is measured, its value is displayed on the LCD and data is sent to the UART. When the temperature is too high, the LED will start blinking.

1. Scheme of temperature meter. The image can be drawn on a computer or by hand. Always name all components and their values.
![sch7](https://user-images.githubusercontent.com/77580298/140944642-fa731fa4-e49a-44a9-a033-4e49f2dcf5d4.png)

