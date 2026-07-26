# Simple CPU

The key component in any computer is the _Central Processor Unit_ or CPU. This does all the calculating and co-ordination for the entire computer.

In previous notes we have seen how basic memory elements work (latches and flip-flops). On their own, this would not be very useful. But we can combine several memory elements together to create a register, a very fast but very small memory store. If we wanted to do a calculation, we could put numbers in two registers and if we knew how to do so, we could add them together and put the result in a third register.

We have also seen how we can use simple circuits to add or subtract two numbers. If you can add, you can multiply, this is _multiplication by successive addition_. We can also use some Boolean maths to make essentially the same circuit do subtraction. If we can do subtraction, we can also do _division by successive subtraction_. So our simple adder can be quite a powerful calculating circuit. In a CPU the circuitry to do these calculations is referred to as an _Arithmetic Logic Unit_ or ALU.

Before we could make a useful calculating machine, we need some way to tie all of these things together. The pathways which allow parts of a computer to communicate with other parts of the computer are called a _bus_.

It would be nice if we knew when things worked or didn’t work, if we had some _status flags_ to indicate when a calculation fails or returns a number that is too big.

The final thing we are going to need is some _control logic_ to hang all these things together and to synchronize everything we want to happen. 

So here is my block diagram for a simple CPU!

<figure>
<img src = "https://jor-donegal.github.io/CPUBasics26/images/fig25.jpg">
<figcaption>fig 25. ALU block diagram.</figcaption>
</figure>

You already know how to build one of these! We know how to make a register and we know how to make an adder/subtractor. So all we really need to do is to hang it all together. On the next page there is a diagram of a 4 bit adding/subtracting machine that I build in Cedar Logic. You may think this is not very impressive, but remember, the world’s first micro-processor was an Intel 4004, a 4 bit processor built for early calculators.

<figure>
<img src = "https://jor-donegal.github.io/CPUBasics26/images/fig26.jpg">
<figcaption>fig 26. ALU circuit.</figcaption>
</figure>

I test the circuit using simple addition. 4 + 5 = 9. In binary that would be 0100 + 0101 = 1001

<figure>
<img src = "https://jor-donegal.github.io/CPUBasics26/images/fig27.jpg">
<figcaption>fig 27. ALU circuit addition test.</figcaption>
</figure>

OK, let us see if the status flag works. 10 + 12 = 22, in binary 1010 + 1100 = 10110. This is too big for a 4 bit calculation!

<figure>
<img src = "https://jor-donegal.github.io/CPUBasics26/images/fig28.jpg">
<figcaption>fig 28. ALU circuit overflow test.</figcaption>
</figure>

The calculation actually worked, the carry out/status flag is 1 and the result is 0110, add the two together and it give 10110, which is correct. However, this is a four bit calculator. Whenever you go over the correct register size that is treated as an _overflow_ and is an error condition. Status flag worked!

On a real CPU, we have a range of status flags. In fact, after every instruction is carried out, flags are set in a dedicated flag register, which can then be checked programmatically.

Final test, let’s see how we do with a subtraction. 10 – 4 = 6. In binary 1010 – 0100 = 110.

<figure>
<img src = "https://jor-donegal.github.io/CPUBasics26/images/fig29.jpg">
<figcaption>fig 29. ALU circuit subtraction test.</figcaption>
</figure>

The result seems correct again. Notice however that the status flag is lit. Whenever we do a 2’s complement calculation on hardware, one of the rules is “discard the carry out”. So we have what looks like an overflow even though the calculation is perfect. In a real CPU we could add a single logic gate to discard the status output if we were doing a subtraction. What gate would that be?

There are a few differences between our simple CPU and a real, usable CPU/computer. Most computers will require more functionality than add and subtract. For us to do repetitive addition, we would need to build additional circuitry. We could load the number to be multiplied into register A and the number it is to be multiplied by in register B. Then we would need the digital logic to add A to A, B number of times. Not a lot of circuitry, but more than we can cover in a this brief summary. For every instruction which we add in hardware, we make the CPU bigger, more expensive, more complex, and more power-hungry. There has been a debate for decades now as to which is the correct approach. 

Processors which have few instructions but are fast and cheap are called _Reduced Instruction Set_ or RISC. Expensive processors which have billions of transistors and hundreds of instructions are call _Complex Instruction Set_ or CISC. 

All modern PCs use CISC processors. All modern smartphones use RISC. Tablets are a mix, Apple/Android all use RISC, some Windows tablets use CISC.

In a real computer, we need somewhere to keep our instructions (or programmes) and our data. 
