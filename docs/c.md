# Two's complement

_Two's complement_ is the most common method computers use to represent signed integers, positive and negative binary numbers. It has the advantage that the same hardware can perform addition and subtraction without needing separate logic for negative numbers.

- Positive numbers are stored as ordinary binary values.
- To get one's compliment, invert all the bits.
- To get two's complement, add 1

As an example for my four bit computing, consider the number 5<sub>10</sub>

| Decimal          | Binary      |
| ---------------- | ----------- |
| 5                | 0101        |
| one's compliment | 1010        |
| two's compliment | 1011        |

Trying a subtraction calculation, I will add -3<sub>10</sub> (the two's complement of 3) to 7<sub>10</sub>

| Decimal          | Binary      |
| ---------------- | ----------- |
| 7                | 0111        |
| 3                | 0011        |
| -3               | 1101        |

 Working out

 0111 + 1101 = 0100 = 4<sub>10</sub>

 One of the rules in two's compliment is to discard any biy that is carried.
