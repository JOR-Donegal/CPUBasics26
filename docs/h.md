# High level CPU

The key component in any computer is the Central Processor Unit or CPU. This does all the calculating and co-ordination for the entire computer.

In previous notes we have seen how basic memory elements work (latches and flip-flops). On their own, this would not be very useful. But we can combine several memory elements together to create a register, a very fast but very small memory store. We have also seen how we can use simple circuits to add two numbers together and we have built and manipulated an Arithmetic Logic Unit or ALU. We have taken a look at main memory and at this stage you should understand how memory stores data in fixed sizes (nibble, bytes or words) in unique addresses. With these elements, we have the basic ingredients, but we are missing the key elements to tie it all together to make a workable computer system. Let’s do that now!

Firstly, we need to get an idea of how a CPU functions. It’s actually very simple and it’s called the _fetch-execute cycle_; or sometimes the _fetch-decode-execute cycle_. A CPU runs like clockwork (literally, everything runs off an electronic pulse called a clock). A computer programme is a list of instructions which the CPU will run through in sequence.

<figure>
<img src = "https://jor-donegal.github.io/CPUBasics26/images/fig30.jpg">
<figcaption>fig 30. The fetch-execute cycle.</figcaption>
</figure>

Let’s imagine we have a programme with 20 steps, starting at step zero.

We need to keep track of where we are in the sequence and to do that we have a special register called the _programme counter_ or PC, initially set at zero (or to the location of the start of the programme). As programmes run sequentially, the PC will normally have an increment function.

To fetch an instruction from memory, we transfer the contents of the programme counter to another special register, the _Memory Address Register_ or MAR. The MAR can assert an address on to the _address bus_, which will control where main memory points to. The contents of that memory location will then be available on the _data bus_. These contents can then be read by a special register, the _Memory Buffer Register_ or MBR.  The contents of the MBR then get transferred to another special register, the _Current Instruction Register_ of CIR. The instruction in the CIR is one of the instructions in the CPUs instruction set. It might be a command like ADD, SUBTRACT, LOAD, etc. We execute this command and then increment the programme counter and run through another cycle. The CPU just keeps doing this……forever!

<figure>
<img src = "https://jor-donegal.github.io/CPUBasics26/images/fig31.jpg">
<figcaption>fig 31. The fetch-execute cycle registers.</figcaption>
</figure>


There is a simple algebra we can use to describe what is going on. We use names to refer to registers and memory and we use names [in square brackets] to refer to the contents of the register or memory. We use arrows to indicate the flow of data. So what we did above could be described as shown.

````
MAR ← [PC]
PC ← [PC] + 1
MBR ← [Memory]
CIR ← MBR
````

Next we need to look at how the instruction in the CIR gets executed.

The CPU needs to be able to “understand” what the instruction means. In reality, there is some decoder logic which looks at the bits in the instruction and activates blocks of digital logic based on what the instruction was. In previous notes, we saw an adder or subtractor. Suppose we said that bit zero of the instruction in the CIR would get hooked up to the subtract button of the ALU. In this case, any instruction with bit 0 = 0 would activate the add functionality. Any instruction with bit zero = 1 would activate the subtract functionality. We can encode a different instruction for every combination of binary digits in the CIR. An eight bit CIR would give us the ability to encode 28 or 256 different instructions.

An instruction to ADD or SUB (subtract) on its own would have no utility; add what? For most instructions we have to pass the values that we want the instruction to work on, for example, the two numbers we want to add together. The data an instruction will execute against are called operands. For example, the ADD instruction 0x00 might be an instruction which means “take the two next values in memory after this instruction and add them together”. Or for a multiply instruction, take the value in a general purpose register and successively add the contents of the accumulator that many times.
The next question…where do we put the results of a calculation?

Many processors support the idea of a special register called the _accumulator_. This is the key register where we perform calculations or place our results.  

The ALU may be built specifically to work with the accumulator.

Alternatively, some processors have many general purpose registers. An ADD instruction might be specifically designed to take the contents of two specified general purpose registers and put the result in the accumulator.

Your smartphone and the ubiquitous Raspberry Pi both use ARM processors. The old 32 bit versions had 16 registers which can be used for almost any purpose. The more modern chips have more.

<figure>
<img src = "https://jor-donegal.github.io/CPUBasics26/images/fig32.jpg">
<figcaption>fig 32. ALU and the fetch-execute cycle.</figcaption>
</figure>

We have already looked at simple models of the ALU and there isn’t that much more to add. We know that the ALU has control inputs to determine what functions it will run (e.g. ADD, SUB, MULT, DIV). 

We also know that it needs inputs to provide it with _operands_.

It also has to have a way of getting the results out. In our examples, we show all these separately. In real processors, there is great variation in how this is done.

<figure>
<img src = "https://jor-donegal.github.io/CPUBasics26/images/fig33.jpg">
<figcaption>fig 33. Simple bus arrangement.</figcaption>
</figure>

In reality, although we might have three internal busses connecting to the ALU, there is only going to be one data bus in the computer, which everything shares. At some point, the data for Bus A and B will have to come into the processor and the data from Bus C will have to be written back to memory.

Our control logic orchestrates all this via a device called a multiplexer. On the diagram, why do we show only two select lines?

<figure>
<img src = "https://jor-donegal.github.io/CPUBasics26/images/fig34.jpg">
<figcaption>fig 34. Multiplexer.</figcaption>
</figure>

The final components we need to have before we can have a working data bus is the buffer or tri-state. Only one device can put information on a data or address bus, if more than one device asserts the bus, there will be chaos!

We have a component called a tri-state which is like an electronic switch. When you need to connect a device to the data bus, you enable the tri-states which connects each line in the bus to the device.

When you no longer want to connect to the bus, you disable the tri-state.

<figure>
<img src = "https://jor-donegal.github.io/CPUBasics26/images/fig35.jpg">
<figcaption>fig 35. A tristate.</figcaption>
</figure>

A tri-state can have an output of zero or one or it can be switched off; hence the name!
