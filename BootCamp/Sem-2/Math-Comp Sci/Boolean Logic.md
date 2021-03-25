# Boolean Logic

Boolean logic is represented as true and false. It is the heart of computer science.

In boolean logic, boolean values may be expressed as TRUE and FALSE, or 1 and 0.



## Boolean Operations

### NOT AND OR XOR

#### Not relation and operators

NOT is a unary boolean relation (meaning it is evaluated on one expression instead of two)

NOT gives the opposite of the value on which it is applied (NOT true = false, NOT false = true)

Symbols that denote NOT:	~ or ! or ¬



#### AND

Both values must be true for AND to evaluate to true

Symbols that denote AND: 	^ or . or &

| p    | q    | p^q  |
| ---- | ---- | ---- |
| T    | T    | T    |
| T    | F    | F    |
| F    | T    | F    |
| F    | F    | F    |



#### OR

One of the other of the values must be true for OR to evaluate to true (at least one)

Symbols that denote OR: 	∨ or || or +

| p    | q    | p ∨ q |
| ---- | ---- | ----- |
| T    | T    | T     |
| T    | F    | T     |
| F    | T    | T     |
| F    | F    | F     |



#### XOR

One or the other of the values **but not both** must be true for XOR to evaluate to true (the two values must be different)

Symbols that denote XOR: 	⊕ or ⊻ or ≢

| p    | q    | p⊕q  |
| ---- | ---- | ---- |
| T    | T    | F    |
| T    | F    | T    |
| F    | T    | T    |
| F    | F    | F    |



### Implication and Evidence

#### Implication

Implication says that if p is true, then q is true. It is only false when p is true and q is false. 
Written as p ⇒  q

*If p is false, q can be either true or false, and the implication is still true*

Example: I will bring an umbrella if it is raining.

*(I may still bring my umbrella if it isn't raining but if it is raining and I don't bring my umbrella, the implication is false)*

| p    | q    | p⇒q  |
| ---- | ---- | ---- |
| T    | T    | T    |
| T    | F    | F    |
| F    | T    | T    |
| F    | F    | T    |

##### Implication can be tricky

a ^ !b ⇒ c

When is this statement false (what must the values of a, b and c be)?

Break it down to solve it:

- When is the implication false?
  - When the left side is true and the right side is false
- When is AND true?
  - When the left and right side are both true
- So what must 'a' be?
  - TRUE (or 1)
- So what must 'be' be?
  - FALSE (or 0)
- So what must 'c' be?
  - FALSE (or 0)

Therefore the statement is false when: a=1, b=0, c=0



#### Equivalence

Equivalence says that q is true if and only if p  is true. Written as: p <=> q

*Either both p and q are true or both false for equivalence to evaluate to true*

Example: I will work if and only if it is a weekday.

*(if it is a weekday, I will always work. If it is not a weekday, I will never work.)*

| p    | q    | p<=>q |
| ---- | ---- | ----- |
| T    | T    | T     |
| T    | F    | F     |
| F    | T    | F     |
| F    | F    | T     |



## Bitwise Operations

We can apply logical operations to a series of bits (to a binary number)

11001100 AND 111010

1st  number - 1100110

2nd Number - 0111010

Answer -		  0100010



1100110 OR 111010

1st  number - 1100110

2nd Number - 0111010

Answer -		  1111110



1100110 XOR 111010

1st  number -  1100110

2nd Number - 0111010

Answer -		  1011100



What about 38 XOR 23?

1. Convert to binary
2. XOR
3. Convert back to decimal

1. 100110
   010111
2. 110001
3. 49



## Logic Statements

Syntax used to express complex logic statements with a combination of symbols and logical operators

- Symbols represent statements that evaluate to true
- Operators used include AND, OR, NOT, XOR (and any of the symbols that can represent those operators)
- Not an if/else construct - something more general

#### Example

Statements:

- I will go to the movies if I'm off work, Star Wars is showing, the theatre is open, and they have choc tops
- I will go to the park if it's sunny, I'm off work, and I am not sick

Symbols:

w: I'm working

m: Star Wars is showing at the theater

t: the theater is open

c: the theatre has choc tops

r: it's raining

s: I'm sick



!w & m & t & c - I will go to the movies

!r & !w & !s - I will go to the park

(!w & m & t & c) || (!r & !w & !s)