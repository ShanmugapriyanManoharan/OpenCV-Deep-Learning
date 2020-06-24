# Matlab Practice

## Lesson 3

### A Simple Function

1. Write a function called tri_area that returns the area of a triangle with base b and height h, where b and h are input arguments of the function in that order.

Code:
```
function ar = tri_area(b,h)
ar = (1/2)*b*h;
end
area = tri_area(5,4)
```
Output:
```
area =

    10
```

### Multiple Outputs

2. Write a function called corners that takes a matrix as an input argument and returns four outputs, the elements at its four corners in this order: top_left, top_right, bottom_left,
and bottom_right (Note that loops and if-statements are neither necessary nor allowed as we have not covered them yet.). See an example run below:

Example:
```
[a, b, c, d] = corners([1 2; 3 4])
a = 
	1
b =
	2
c = 
	3
d =
	4
```
Code:
```
function [top_left, top_right, bottom_left, bottom_right] = corners(Mat)
[rows, columns] = size(Mat);
top_left = Mat(1,1);
top_right = Mat(1,columns);
bottom_left = Mat(rows,1);
bottom_right = Mat(rows, columns);
end

A = randi(100,4,5)
[top_left, top_right, bottom_left, bottom_right] = corners(A)
B = [1; 2]
[top_left, top_right, bottom_left, bottom_right] = corners(B)
```
Output:
```
A =

    57    51    56    63    17
    66    37    88    74    32
    91    81    85    46     3
    22    97    18    54    75


top_left =

    57


top_right =

    17


bottom_left =

    22


bottom_right =

    75


B =

     1
     2


top_left =

     1


top_right =

     1


bottom_left =

     2


bottom_right =

     2
```

### Lesson 3 Wrap-Up

3. Write a function called taxi_fare that computes the fare of a taxi ride. It takes two inputs: the distance in kilometers (d) and the amount of wait time in minutes (t). The fare is
calculated like this:
-> the first Km is $5
-> every additional Km is $2
-> and every minute of wait is $0.25

Once a Km is started, it counts as a whole (Hint: consider the ceil built-in function). The same rule applies to wait times. You can assume that d > 0 and t >= 0 but they are not
necessarily integers. The function returns the fare in dollars. For example, a 3.5 Km ride with 2.25 minutes of wait costs $11.75. Note that loops and if-statements are neither
necessary nor allowed.

Code:
```
function fare = taxi_fare(d, t)
d = ceil(d-1);
t = ceil(t);
fare = 5 + (2*d) + (t*0.25);
end
fare = taxi_fare(3.5,2.25)
```
Output:
```
fare =

   11.7500
```