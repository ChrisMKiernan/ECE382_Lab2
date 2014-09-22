## ECE382 Lab2 - Cryptography

Goal: to decrypt a message using an XOR decrypt method with a key (or not). 

### Design

To design the decrypting program several steps are involved. One is to determine how long the message is. When we save the message in ROM by using .byte, the message is stored starting at 0xc000. This moves our program counter to the end of the message. In order to determine how long the message is, I stored the value of the program counter and counted down until the end of the message. 

Another problem we have to solve is to determine how to use a key of a different length with the message (for B functionality). To do this I stored the key into 3 different memory locations. When I had to decrypt individual characters, I incremented the memory pointer of the key for each new character loop until all 3 of the key values had been used. I saved each value into RAM as they were decrypted, then I reran the program until the end of the message. 

### Implementation

All of the steps described above were implemented using Code Composer Studio v6. In order to get a true value of how long the message was, I used the BIC (bit clear) function with the value of 0xc000. This erased the c at the beginning of the value, so that I could find the difference between the beginning Program Counter value and the beginning of ROM, which was actually more applicable. I used several INC and DEC functions to keep track of the key, the memory pointer for the message, and the length of the message, so that my program would not run too long. 

### Problems

A problem I had in my decrypt code was that I stored the values of the key in reverse order of what I needed to use them. This was a remnant from trying to use indexed addressing with a memory pointer that stayed stagnant at 0x0200 and a separate counting register to keep the value of the key. However, this was overly complicated and actually didnt work as expected, so I instead incremented the memory pointer and checked that value against 0x0203, which should be the end of the key. When first implementing this design, though, I forgot to rearrange my initial locatoins/values of the key, leading to the key being read backwards.

### Functionality

Required functionality was skipped and I went directly to B functionality, which was checked after class LSN12, 17 Sep
