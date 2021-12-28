# 8-bit signed sequential multiplier/divider

#### How to build and use the code

To build the code: you will simply download this GitHub repo and run it using Vivado.
To test the code: First, use the toggle switches of the FPGA to input two 8 bit signed values. 
Then, press on the key ’n’ if you wish to perform multiplication and the key ‘o’ if you wish to perform division.  
The decimal output of each operation will be displayed on the four digit seven segment display of the FPGA. 
Press on ‘m’ if you would like to reset the whole operation and the value displayed the LEDs will return to zero.

#### Challenges, Assumptions & Design Limitations

We faced a lot of problems with the UART. After a lot of debugging and various tests,
we discovered that not all the keypresses were working properly. Thus, we depended
on the UART for only three keys (the reset button and the enable signals for
multiplication and division). For the inputting of our two 8-bit binary numbers, we
preferred to use the toggle switches on the FPGA to ensure full functionality. Even after we followed this approach, we were still facing other obstacles. We had a
problem in catching the enable signals of the multiplication and the division. We
assumed at first that once we press the key that’s responsible for triggering the value of
the start_mult or start_div, both the product p and the quotient Q will retain their old
values, however, this was not clearly the case. When debugging the code, we
concluded that after start_mult and start_div are pressed (receive the values of 1),
they go back to zero with the raise of our hands from the pressed key, and thus p, and
Q go back to zero. We managed to solve this problem by using a small FSM that
checks in which state we are (multiplication, division, or reset), and then stays in the
same state as long as nothing is pressed.
Further, we assumed that since we cannot display a negative sign on the FPGA, we
decided to display the decimal value of the 2s complement of the product or quotient.
