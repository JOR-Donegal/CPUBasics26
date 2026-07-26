# Practical Memory

The first computer systems (e.g. ENIAC) required programmes to be hard wired, literally with jumper cables, dials and switches. A computer at the time looked like something out of a bad sci-fi movie!

From 1944 and the development of the EDIVAC computer, work began on holding computer programmes and data in electronics memory. In 1945 Jon Von Neumann proposed that a working computer system should consist of a processing unit or ALU, a control unit, and memory. We have looked at the ALU and at control in previous notes, let’s take a look at memory!
Firstly some terminology.

- A bit is a single binary digit and can be a one or a zero
- A nibble is a group of 4 bits
- A byte is a group of 8 bits
- A word is a group of 16 or more bits, we can have 32 bit words, 64 bit words etc.

In previous notes, we have built the bones of a simple 4 bit computer. Can we provide this computer with a small amount of 4-bit memory?

<figure>
<img src = "https://jor-donegal.github.io/CPUBasics26/images/fig19.jpg">
<figcaption>fig 19. A four bit register.</figcaption>
</figure>

In fact, the design is that of a 4 bit register. 

As previously, we will clock the circuit. When write is enabled, whatever is on the input bus will be copied to the registers. They can then be read at the output bus an unlimited number of times.

Once write enabled is switched off, any changes in the input bus will not be copied to the memory element. 

So now we have a single memory element, good to store a single nibble of data. How do we scale that up to make a useful quantity of memory?

When we design memory, we tend to do so as a grid of rows and columns. Imagine a spreadsheet where we lay out the memory. We have a 4 bit computer, each column could be one 4 bit nibble and we can populate the grid with ones and zeros.

<figure>
<img src = "https://jor-donegal.github.io/CPUBasics26/images/table4.jpg">
<figcaption>Table 4. Row and Column select.</figcaption>
</figure>

We can only read/write one nibble at a time, so we are going to need to be able to select which nibble we want to read from. Let’s call that the address of the nibble of data. So we need some way to select the correct address.

<figure>
<img src = "https://jor-donegal.github.io/CPUBasics26/images/table5.jpg">
<figcaption>Table 5. Memory address select.</figcaption>
</figure>

So how do we select only one column (nibble) on at a time?

An AND gate makes a perfect switch, only enabling a column (nibble) when the enable line is on. Write is only enabled when the enable line is on AND write is enabled AND the clock is high. 

However, we will also have to put a gate on each output, so that the only nibble which sends an output to the end is the activated one.

This requires a gate per column to select for write enable and a gate per memory element or bit. 

<figure>
<img src = "https://jor-donegal.github.io/CPUBasics26/images/fig20.jpg">
<figcaption>fig 20. Memory select logic.</figcaption>
</figure>

If we duplicate this column, we can create a new memory address (nibble) of data per column. Only one column should be active at a time, so all the outputs of all the other columns will be zero. If we OR all the outputs for each bit in the nibble, we will only get the output from the enabled column.

<figure>
<img src = "https://jor-donegal.github.io/CPUBasics26/images/fig21.jpg">
<figcaption>fig 21. 3x4 Memory.</figcaption>
</figure>

We have one more step to look at. There is a major scalability problem with this circuit!

We need an address line per address.

Imagine if we had a 256 addresses for data, we would need 256 lines on an address bus! But we can count from 0-255 using only eight bits (28=256). Wouldn’t it be more useful to have an address bus where we carried only the binary number of the address and then translated it into an enable line at the memory array?

This type of circuit would be called a 2-to-4 line decoder. It would be typical of the kind of logic on the memory bus of a computer to allow the CPU to select exactly which memory address it wanted to read or write to/from.

On a 32 bit computer we need 32 address line to address 4,294,967,296 memory locations!

<figure>
<img src = "https://jor-donegal.github.io/CPUBasics26/images/fig22.jpg">
<figcaption>fig 22. 2-to-4 line decoder.</figcaption>
</figure>

Here is our finished circuit, including the memory decoder. We only have 3 addresses available in memory, so we have one spare address enable line.

<figure>
<img src = "https://jor-donegal.github.io/CPUBasics26/images/fig23.jpg">
<figcaption>fig 23. Final Circuit.</figcaption>
</figure>

This is a very small example, but it gives you an idea of how to construct a kind of memory called _Static Random Access Memory_ or SRAM. This example is too small to be practical, but it gives you an idea how you might build working memory. As you can see, there are many components per bit, so this kind of memory is very expensive and is used for specialist purposes only, mostly for cache, which we will deal with in a later lecture.

Most of the memory in a conventional computer is made of fewer components, perhaps two transistors and a capacitor per bit….but the row and column selection logic will be exactly the same. This kind of memory is called _Dynamic Random Access Memory_ or DRAM, and we will see this in detail later in the module.

As with all things complex, once we understand how memory works and what the terminology is around it, we can create an abstraction to simplify diagrams and make it easier to get an overview of what is going on. A memory block might be shown as something like this.

<figure>
<img src = "https://jor-donegal.github.io/CPUBasics26/images/fig24.jpg">
<figcaption>fig 24. Block diagram.</figcaption>
</figure>

A final word….

An architecture where programmes and data share memory is still called a _Von Neumann architecture_. There is another option, the _Harvard architecture_. In this type of computer, the memory which holds programmes is completely separate from the memory to hold data. From a security perspective, there may be much to be said for this.
