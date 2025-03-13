# CMPS 2200 Assignment 2

**Name:** Jaedan Curcio

In this assignment we'll work on applying the methods we've learned to analyze recurrences, and also see their behavior
in practice. As with previous
assignments, some of of your answers will go in `main.py` and `test_main.py`. You
should feel free to edit this file with your answers; for handwritten
work please scan your work and submit a PDF titled `assignment-02.pdf`
and push to your github repository.


## Part 1. Asymptotic Analysis

Derive asymptotic upper bounds of work for each recurrence below.

* $W(n)=2W(n/3)+1$

.

Leaf dominant as work grows with n - Bound is work at lowest level

Lowest level at $n/3^k = 1$, so $k = log3(n)$

Number of subproblems at lowest level = $2^k$, so total work is $2^{log3(n)}$, or $O(n^{log3(2)})$

.
 
* $W(n)=5W(n/4)+n$

.

Leaf dominant as work grows with n - Bound is work at lowest level

Lowest level at $n/4^k$ = 1, so $k = log4(n)$

Number of subproblems at lowest level = $5^k$, so total work is $5^{log4(n)}$, or $O(n^{log4(5)})$

. 

* $W(n)=7W(n/7)+n$

.  

Balanced, work = work @ each level * lowest level

Asymptotic upper bound = $O(n log(n))$

.

* $W(n)=9W(n/3)+n^2$

.

Balanced, work = work @ each level * lowest level

Asymptotic upper bound = $O(n^2 log(n))$
 
.

* $W(n)=8W(n/2)+n^3$
.  

Balanced, asymptotic upper bound = $O(n^3 log(n))$ 

. 


* $W(n)=49W(n/25)+n^{3/2}\log n$
.  

Root dominant, upper bound is $O(n^{3/2}\log n)$

.  

* $W(n)=W(n-1)+2$

.

$W(n-1) = W(n-2) + 2 -- W(n) = W(n-2) + 4$

$W(n) = W(n-k) + 2k$ ...  @ base case $n-k = 1$, so $k = n-1$

$W(n) = W(n - (n-1)) + 2(n-1) = W(1) - 2n - 2 = O(n)$

.

* $W(n)= W(n-1)+n^c$, with $c\geq 1$

.  

$W(n-1) = W(n-2) + (n-1)^c -- W(n) = W(n-2) + (n-1)^c + n^c$

@ base case, $W(n) = W(1)$ plus the sum from k=0 to k=n of $k^c$

Power sums are $O(n^{c+1})$, so final equation is $W(n) = W(1) + O(n^{c+1})$, so the upper bound is $O(n^{c+1})$

. 

* $W(n)=W(\sqrt{n})+1$
.


$W(\sqrt{n}) = W(\sqrt{\sqrt{n}}) + 1$

$W(n) = W(\sqrt{\sqrt{n}}) + 2$

$W(n) = W(n^{1/2^k}) + k$

$n^{1/2^k} = W(1) = (1/2^k) log(n) = O(1)$

$O(2^k) = log n, k = O(log( log (n))$

Root work is O(1), so equation is leaf dominant, so bound is $O(log( log (n))$

. 


## Part 2. Algorithm Comparison

Suppose that for a given task you are choosing between the following three algorithms:

  * Algorithm $\mathcal{A}$ solves problems by dividing them into
      five subproblems of half the size, recursively solving each
      subproblem, and then combining the solutions in linear time.
    
  * Algorithm $\mathcal{B}$ solves problems of size $n$ by
      recursively solving two subproblems of size $n-1$ and then
      combining the solutions in constant time.
    
  * Algorithm $\mathcal{C}$ solves problems of size $n$ by dividing
      them into nine subproblems of size $n/3$, recursively solving
      each subproblem, and then combining the solutions in $O(n^2)$
      time.

    What are the asymptotic running times of each of these algorithms?
    Which algorithm would you choose?


 A: $W(n) = 5W(n/2) + n$

Leaf dominant, work is $O(n^{log2(5)})$

.  

B: $W(n) = 2W(n-1) + 1$

$W(n-1) = 2W(n-2)) + 1$

$W(n) = 4W(n-2)) + 2$

$W(n) = 2^{k}W(n-k) +$ sum from 0 to k-1 of $2^c$

$n-k = 1, k = n-1, $ k is $O(n)$, summation is $O(2^n)$ which is the asymptotic bound

 
.

C: $W(n) = 9W(n/3) + n^2$

Balanced, work is $O(n^2 log (n))$


Algorithm $C$ is the best choice.

.




## Part 3: Parenthesis Matching

A common task of compilers is to ensure that parentheses are matched. That is, each open parenthesis is followed at some point by a closed parenthesis. Furthermore, a closed parenthesis can only appear if there is a corresponding open parenthesis before it. So, the following are valid:

- `( ( a ) b )`
- `a () b ( c ( d ) )`

but these are invalid:

- `( ( a )`
- `(a ) ) b (`

Below, we'll solve this problem three different ways, using iterate, scan, and divide and conquer.

**3a. iterative solution** Implement `parens_match_iterative`, a solution to this problem using the `iterate` function. **Hint**: consider using a single counter variable to keep track of whether there are more open or closed parentheses. How can you update this value while iterating from left to right through the input? What must be true of this value at each step for the parentheses to be matched? To complete this, complete the `parens_update` function and the `parens_match_iterative` function. The `parens_update` function will be called in combination with `iterate` inside `parens_match_iterative`. Test your implementation with `test_parens_match_iterative`.


.  
. 



**3b.** What are the recurrences for the Work and Span of this solution? What are their Big Oh solutions?

**Recurrence for work is $W(n) = 2W(n/2) + 1$, which is $O(n)$. The span recurrence is $S(n) = S(n/2) + 1$, which is $O(log(n))$**

.  
. 



**3c. scan solution** Implement `parens_match_scan` a solution to this problem using `scan`. **Hint**: We have given you the function `paren_map` which maps `(` to `1`, `)` to `-1` and everything else to `0`. How can you pass this function to `scan` to solve the problem? You may also find the `min_f` function useful here. Implement `parens_match_scan` and test with `test_parens_match_scan`

.  
. 



**3d.** Assume that any `map`s are done in parallel, and that we use the efficient implementation of `scan` from class. What are the recurrences for the Work and Span of this solution? 

**Work is $O(n)$ since you must check every input, and span is $O(log(n))$**

.  
.  




**3e. divide and conquer solution** Implement `parens_match_dc_helper`, a divide and conquer solution to the problem. A key observation is that we *cannot* simply solve each subproblem using the above solutions and combine the results. E.g., consider '((()))', which would be split into '(((' and ')))', neither of which is matched. Yet, the whole input is matched. Instead, we'll have to keep track of two numbers: the number of unmatched right parentheses (R), and the number of unmatched left parentheses (L). `parens_match_dc_helper` returns a tuple (R,L). So, if the input is just '(', then `parens_match_dc_helper` returns (0,1), indicating that there is 1 unmatched left parens and 0 unmatched right parens. Analogously, if the input is just ')', then the result should be (1,0). The main difficulty is deciding how to merge the returned values for the two recursive calls. E.g., if (i,j) is the result for the left half of the list, and (k,l) is the output of the right half of the list, how can we compute the proper return value (R,L) using only i,j,k,l? Try a few example inputs to guide your solution, then test with `test_parens_match_dc_helper`.



.  
. 





**3f.** Assuming any recursive calls are done in parallel, what are the recurrences for the Work and Span of this solution? What are their Big Oh solutions?

**The recurrences are the same as for the iterative solution, which are $W(n) = 2W(n/2) + 1$ and $S(n) = S(n/2) + 1)$, which are $O(n)$ and $O(log(n))$ respectively.**

.  
. 


 
 


