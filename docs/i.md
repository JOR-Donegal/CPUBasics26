# Finally

So now let’s bring together everything we have learned, to sketch a fully working CPU, with external connectivity.

<figure>
<img src = "https://jor-donegal.github.io/CPUBasics26/images/fig36.jpg">
<figcaption>fig 36. Summary - CPU.</figcaption>
</figure>

- We have a range of busses interconnecting the internal components within the CPU. 
- The internal data bus within the CPU would allow a vale to be transferred to/from the accumulator to/from almost any register.
- The MBR is bi-directional, we can either read data off the data bus or write data to the data bus, based on the address asserted in the MAR.
- The external data, address and control bus are shared amongst all the components of the computer.
- Everything is orchestrated by the control unit, both inside the CPU and via the external control bus.
- There will be buffering between each internal component and the internal data bus. Only one internal component will be able to write to the internal data bus at a time. This is determined by the control unit.
- Multiplexer/De-multiplexer blocks will be used to enable multiple devices to share the same busses
- There will also be buffering between memory chips and the data bus. Complex encoder/decoder logic allows the correct memory chips to be selected and the correct rows/columns activated.

That’s it for simple CPU design. We now having a working central processor. Keep in mind though, I have made this as simple as possible, with the minimum components to describe a workable system. We have only scratched the surface. A real CPU has a great deal more complexity and has many more add-ons to increase performance. However, if you can follow what we have covered to date, the add-ons will all make sense!