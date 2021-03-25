



# Matrix Maths

A matrix is a two dimensional array of numbers

Matrixes have multiple rows and columns (2x3)

To type this in code `$A\ =\ [\begin{matrix}6&4&24\\1&-9&8\end{matrix}]$`

$A\ =\ [\begin{matrix}6&4&24\\1&-9&8\end{matrix}]$

A 0,0 = 6

A 0,1 = 4

A 0,2 = 24

A 1,0 = 1

A 1,1 = -9

A 1,2 = 8

Declared in a program, this matrix would look like this:
matrix = [ [ 6 ,4 , 24], [ 1, -9, 8] ]

To access 6 it would be `matrix[0][0]`

#### Why?

You use them to solve some problems. For example if you are selling items, calculating sales over a period of time would likely be done using matrices.

### Addition

Adding matrices requires that the matrices are the same dimensions - that they have the same number of rows and columns. Just add each element from each matrix and store the sum in the result matrix

[ 3 , 8, 4, 6] + [ 4, 0, 1, -9] =  [ 7, 8, 5,- 3]

### Subtraction

Subtracting matrices also requires the same ruling as the above but with subtraction.

[ 3 , 8, 4, 6] + [ 4, 0, 1, -9] =  [ -1, 8, 3, 15]

### Scalar multiplication

Scalar multiplication just means multiplying by a constant. Multiply each term in the matrix by the constant to get the result.

2 x  [4, 0, 1, -9] = [8, 0, 2, -18]

2 x A = 2A

### Multiplication (dot product)

Multiplying two matrices is also called finding the **dot product**. To find the dot product, multiple the elements of **each row of the first matrix** with the elements of **each column in the second matrix**.

[\$3, \$4, \$2] x [ [13, 9, 7, 15] , [8, 7, 4, 6] , [6, 4, 0, 3] ] = [\$83, \$63, \$37, \$75]

You get 83 by doing $3 * 13$ + $4*8$ + $2*6$

### Transposing

Transposing a matrix is done by swapping rows and columns. 

$ [ [ 6 ,4 , 24], [ 1, -9, 8] ]^T$ = [[ 6, 1 ], [ 4, -9 ], [  24, 8 ]]

# Example: Tshirt Sales

An online shop sells 3 kinds of tshirts. The prices are given by the following matrix:

[ style1, style2, style3] = [\$5, \$8. \$9]

Over 5 days, the following sales are made:

|           | style 1 | style 2 | style 3 |
| --------- | ------- | ------- | ------- |
| Monday    | 4       | 8       | 3       |
| Tuesday   | 12      | 0       | 5       |
| Wednesday | 3       | 10      | 8       |
| Thursday  | 15      | 4       | 2       |
| Friday    | 5       | 6       | 9       |

You can get the total day sales and week/per style using matrix multiplication.

[ [4, 8, 3] , [12, 0, 5] , [3, 10, 8] , [15, 4, 2] , [5, 6, 9] ]

[\$5, \$8, \$9 ] * [ [4, 8, 3] , [12, 0, 5] , [3, 10, 8] , [15, 4, 2] , [5, 6, 9] ] can not be done so we would transpose this.

[\$5, \$8, \$9 ] * [[4,12,3,15,5],[8,0,10,4,6], [3,5,8,2,9]] = [\$111, \$105 , \$167, \$, 125, \$154 ]