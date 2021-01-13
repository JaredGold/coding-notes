# CS Fundamentals - Bases

A base is a set of digits used to express numeric values.

In base 10, we have 10 digits (0,1,2,3,4,5,6,7,8,9)

With those 10 digits, we can express any numeric value.

When we run out of digits in one place, we move on to the next place:
...7,8,9... 10,11... 99, 100...



## Binary

Decimal is base 10, binary is base 2

Binary has 2 digits - 0 & 1

What happens if we run out of digits?

| Decimal | Binary |
| ------- | ------ |
| 1       | 1      |
| 2       | 10     |
| 3       | 11     |
| 4       | 100    |
| 5       | 101    |



### Place Values - decimal

In any number, the place value is the digit multiplied by it's 'place' in the number

In base 10:

| 10^3 | 10^2 | 10^1 | 10^0 |
| ---- | ---- | ---- | ---- |
| 1000 | 100  | 10   | 1    |
| 5    | 4    | 8    | 0    |



Ex: 5480

The place value of '4' is 4 x 100, because 4 is in the 100's place



### Place Values - Binary

In binary (and every other base), place values are exactly the same - the digit value multiplied by its place in the number, but in binary the digit is always either 1 or 0

Ex: 101100

| 2^5  | 2^4  | 2^3  | 2^2  | 2^1  | 2^0  |
| ---- | ---- | ---- | ---- | ---- | ---- |
| 32   | 16   | 8    | 4    | 2    | 1    |
| 1    | 0    | 1    | 1    | 0    | 0    |

The place value of the first `1` is 1 x 32 = 32 (in decimal)



### Converting from binary to decimal

Same as the process to convert a number from any base to decimal

Calculate the place value for each digit in the number, then add them together

Example: 101110 base 2 = ? base 10

101110 = (1 x 32) + (0 x 16) + (1 x 8) + (1 x 4) + (1 x 2) + (0 x 1)

= 32 + 8 + 4 + 2

= 46



### Converting from decimal to binary - method 1

Example: 19 base 10

What is the largest power of 2 that goes into 19? Put a 1 in that place

Subtract that value from the original value, and do the same for what is left.

| 2^5  | 2^4  | 2^3  | 2^2  | 2^1  | 2^0  |
| ---- | ---- | ---- | ---- | ---- | ---- |
| 0    | 1    | 0    | 0    | 1    | 1    |



### Converting from decimal to binary - method 2

Divide method 

Example: 19

19/2 = 9 R1 | is 9 divisible by 2?

9/2 = 4 R1

4/2 = 2 R0

2/2 = 1 R0

Starting from the last number divided = 1 

Then go from the remainders... 10011



## Hexadecimal

Base 16 has 16 digits:

| Decimal     | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   | 13   | 14   | 15   |
| ----------- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| Hexadecimal | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | A    | B    | C    | D    | E    | F    |

After 9, we use the letters for the remaining digits.



Just like binary, add place values to convert hexadecimal to decimal

Example: 0x2CB = ? base 10

0x2CB = (2x256) + (12x16) +  (11x1)

​	= 512 + 192 + 11 = 715



### Hexadecimal Colors

#0122FF

01 - Red

22 - Green

FF - Blue

Convert to decimal (rgb format) by converting each value to decimal

0x01 = 1 (base 10) 	0x22 = 2x16 + 2 = 34 (base 10)	0xFF = 15x16 + 15 = 255 (base 10)

rgb(1, 34, 255)



### Hex and binary

Notice that 16 = 2^4, so 1 hex digit is equivalent to 4 binary digits

| Hex    | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    |
| ------ | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| Binary | 0000 | 0001 | 0010 | 0011 | 0100 | 0101 | 0110 | 0111 | 1000 | 1001 |

| A    | B    | C    | D    | E    | F    |
| ---- | ---- | ---- | ---- | ---- | ---- |
| 1010 | 1011 | 1100 | 1101 | 1110 | 1111 |

So we can convert every hex digit to four binary digits directly, and every four binary digits to one hex digit

Example: 0x5A3 = 0101 1010 0011 (base 2)



### Convert from one base to another

To convert between non-base 10 numbers, you need to go through a base 10 conversion

Example: 58 base 9 = ? base 5

1. Convert 58 base 9 to decimal
   (5x9) + (8x1) = 45 + 8 = 53
2. Convert 53 base 10 to base 5
   53/5 = 10
   10/5 = 2
   R = 3
   R = 0
   = 203 (base 5)



### Counting

What comes next in hexadecimal?

0,1,2,3,4,5,6,7,8,9,A,B,C,D,E,F,		10,11,12,13,14,15,16,17,18,19,1A..

What comes next in base 13?

0,1,2,3,4,5,6,7,8,9,A,B,C		10,11,12,13,14,15,16,17,18,19,1A..

What comes next in base 4?

0,1,2,3,	10,11,12,13,	20,21,22,23



### Bit shifting

1000 >> 2	Drop the right-most 2 bits (moving all bits to the right 2 places)

​	10 (base 2) = 2 (base 10)

100 << 1		Add 1 zero to the end (moving all bits to the left 1 place)

​	1000 (base 2) = 8(base 10)



