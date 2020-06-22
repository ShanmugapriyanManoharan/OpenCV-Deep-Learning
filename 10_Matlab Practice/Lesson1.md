# Matlab Practice

## Lesson 1
1. We borrowed $1000 at a 10% annual interest rate. If we did not make a payment for two years, and assuming there is no penalty for non-payment, how much do we owe now?
Assign the result to a variable called debt.

Code:
```
p = 1000; r = 0.1; t = 2;
debt = p*((1+r)^t)
```
Output:
```
debt =

   1.2100e+03
```

2.1. As of early 2018, Usain Bolt holds the world record in the men's 100 meter dash. It is 9.58 seconds. What was his average speed in Km/h? Assign the result to a variable
called hundred.
2.2. Kenyan Eliud Kipchoge set a new world record for men of 02 hrs 01 minutes 39 seconds on September 16,2018. Assign his average speed in Km/h to the variable marathon. The marathon
distance is 42.195 Kilometers.

Code:
```
distance = 0.1; time = 9.58/(60*60);
hundred = distance/time
distance = 42.195; time = 7299/(60*60);
marathon = distance/time
```
Output:
```
hundred =

   37.5783


marathon =

   20.8113
```
