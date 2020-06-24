# Matlab Practice

## Lesson 2

### Colon Operator

1.1. Create a vector of all the odd positive integers smaller than 100 in increasing order and save it into variable odds.
1.2. Create a vector of all the even positive integers smaller than or equal to 100 in decreasing order and save it into variable evens.

Code:
```
odds = 1:2:100
evens = 100:-2:2
```
Output:
```
odds =

  Columns 1 through 30

     1     3     5     7     9    11    13    15    17    19    21    23    25    27    29    31    33    35    37    39    41    43    45    47    49    51    53    55    57    59

  Columns 31 through 50

    61    63    65    67    69    71    73    75    77    79    81    83    85    87    89    91    93    95    97    99


evens =

  Columns 1 through 30

   100    98    96    94    92    90    88    86    84    82    80    78    76    74    72    70    68    66    64    62    60    58    56    54    52    50    48    46    44    42

  Columns 31 through 50

    40    38    36    34    32    30    28    26    24    22    20    18    16    14    12    10     8     6     4     2
```

### Matrix Indexing

2. Given matrix A, assign the second column of A to a variable v. Afterwards change each element of the last row of A to 0.

Code:
```
A = [1:5; 6:10; 11:15; 16:20];
A
v = A(:,2)
A(end,:)=0
```
Output:
```
A =

     1     2     3     4     5
     6     7     8     9    10
    11    12    13    14    15
    16    17    18    19    20


v =

     2
     7
    12
    17


A =

     1     2     3     4     5
     6     7     8     9    10
    11    12    13    14    15
     0     0     0     0     0
```

### Matrix Arithmetic

3. Given a Matrix A,
-> Create a row vector of 1's that has same number of elements as A has rows.
-> Create a column vector of 1's that has same number of elements as A has columns.
-> Using matrix multiplication, assign the product of the row vector, the matrix A, and the column vector (in this order) to the variable result.

Code:
```
A = [1:5; 6:10; 11:15; 16:20];
A;
size_A = size(A);
rows_vec = ones(1,size_A(1));
columns_vec = ones(size_A(2),1);
result = rows_vec * A * columns_vec
```
Output:
```
result =

   210
```