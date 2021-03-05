# Week 3 notes of HarvardX's Introduction to Computer Science course

# Topic: Algorithms 

## Big O, Big O notation, and running times 

* Running times: how long an algorithm takes to run given some size of input. 
  * Common examples of running times: 
  * O(n^2)
  * O(nlogn)
  * O(n)
    * (searching one page at a time, in order)
  * O(logn)
    * (dividing the phone book in half each time)
  * O(1)
    * An algorithm that takes a constant number of steps, regardless of how big the problem is

## Linear search, binary search 

* If we want to look for the number zero, for example, we would have to open one door at a time, and if we didn't know anything about the numbers behind the doors, the simplest algorithm would be going from left to right. 
  * So, we might write pseudocode for a `linear search` with: 
  ```
  For i from 0 to n-1
    If number behind i'th door
      Return true
  Return false
  ```
    * We would label each of `n` doors from `0` to `n-1`, and check each of them in order.
    * "Return False" is outside the for loop, since we only want to do that after we've looked bind all the doors. 
    * The big O running time for the algorithm would be O(n), and the lower bound, Big Omega, would be Omega(1). 
  * If we know that the numbers behind the doors are sorted, then we can start in the middle, and find our value more efficiently. 
    * For a `binary search` our algorithm might look like: 
    ```
    If no doors
      Return false
    If number behind middle door
      Return true
    Else if number < middle door
      Search left half
    Else if number > middle door
      Search right half
    ```
  * The upper bound for binary search is O(logn), and the lower bound is also Omega(1), if the number we're looking for is in the middle, where we happen to start.
* With 64 light bulbs, we notice that linear search takes much longer than binary search, which only takes a few steps. 

## Searching with code













