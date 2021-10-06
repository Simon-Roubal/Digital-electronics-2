# Lab 3: YOUR_FIRSTNAME FAMILYNAME

Link to your `Digital-electronics-2` GitHub repository:

   [https://github.com/Simon-Roubal/Digital-electronics-2/tree/main/Lab_03](https://github.com/Simon-Roubal/Digital-electronics-2/tree/main/Lab_03)


### Data types in C

1. Complete table.

| **Data type** | **Number of bits** | **Range** | **Description** |
| :-: | :-: | :-: | :-- | 
| `uint8_t`  | 8 | 0, 1, ..., 255 | Unsigned 8-bit integer |
| `int8_t`   | 8 |  |  |
| `uint16_t` | 16 |  |  |
| `int16_t`  | 16 |  |  |
| `float`    |  | -3.4e+38, ..., 3.4e+38 | Single-precision floating-point |
| `void`     |  |  |  |


### GPIO library

1. In your words, describe the difference between the declaration and the definition of the function in C.
   * Function declaration
   * Function definition

2. Part of the C code listing with syntax highlighting, which toggles LEDs only if push button is pressed. Otherwise, the value of the LEDs does not change. Use function from your GPIO library. Let the push button is connected to port D:

```c
    // Configure Push button at port D and enable internal pull-up resistor
    
    GPIO_config_input_pullup(&PORTD, BUTTON);

    // Infinite loop
    while (1)
    {
         while(GPIO_read(&PIND, BUTTON) == 0)
         {
             _delay_ms(BLINK_DELAY);
             
             GPIO_write_high(&PORTB, LED_GREEN);
             GPIO_write_low(&PORTC, LED_BLUE);
             
             _delay_ms(BLINK_DELAY);
             
             GPIO_write_low(&PORTB, LED_GREEN);
             GPIO_write_high(&PORTC, LED_BLUE);
             
         }
    }
```


### Traffic light

1. Scheme of traffic light application with one red/yellow/green light for cars and one red/green light for pedestrians. Connect AVR device, LEDs, resistors, one push button (for pedestrians), and supply voltage. The image can be drawn on a computer or by hand. Always name all components and their values!

   ![your figure]()
