[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/OlW38W4k)
# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

Mystery Function run time:
The if statement takes constant time. +1
The else statement takes much more. It recursively calls 3 times, each dividing n by 3. So this would be 3T(n/3) similar to divide and conquer sum. 
var count = 0 takes constant time, +1.
The first for loop runs $\ n^2$ times, the second for loop is nested and runs for n times, and the third for loop is nested inside the other two and runs $\ n^2$ times.
$\ n^2 * n * n^2 = n^5 $. Disregarding the constant time, we have the recursive relation of 

T(n) = 1 if $\ n \leq 1. $

$\ T(n) = 3 T(\frac{n}{3}) + n^5$ ; else

Solving Recurrance relation:

$\ 3T(\frac{n}{3}) + n^5 $

$\ = 3 (3 T(\frac{\frac{n}{3}}{3}) +(\frac{n}{3})^5) + n^5 $

$\ = 9 T(\frac{n}{9}) + 3 (\frac{n}{3})^5 +n^5 $

$$\ = 3^i T(\frac{n}{3^i}) +  n^5 \cdot \sum_{j=0}^{i-1} 3^{i} \cdot (\frac{1}{3} )^{5i} $$

To solve for the base case to get our asymptotic complexity, we can substitute in $\ i = log_{3} n$.

$$\ = 3^{log_{3} n} T(\frac{n}{3^{log_{3} n}}) + n^5 \cdot \sum_{j=0}^{{log_{3} n}} 3^{log_{3} n} \cdot (\frac{1}{3})^{log_{3} n} $$

The summation would give us n * $\ \frac{1}{n} $, simplifying to 1, and giving us $\ n^5 *1 $.

$$\= n \cdot T(1) + n^5 $$.

So the runtime analysis for this function is:

$\ n \cdot 1 + n^5 \in O(n^5)$
