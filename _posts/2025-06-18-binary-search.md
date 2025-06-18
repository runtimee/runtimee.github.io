---
layout: post
author: Yan
title: Practical Algorithms - Binary Search
---

Binary search is a fundamental, yet powerful and frequently used algorithm. It has several interesting variations, which are usually skipped in a college CS class or “left as an exercise to the reader”.

It came to me during a coding contest that it is worth the time to possess the full power of binary search with [all the beautiful variations](https://en.wikipedia.org/wiki/Binary_search), while being “practical” without formal math proves (and some horrible 1-indexed array in the math proves, or unnecessary abstraction to relate with binary-tree).


# 1. Basic Format

Given a sorted array of unique integers and a target integer, return the index if the target is found in the array, or -1 if not found.

```python
def binary_search_basic(arr, target):
    low, high = 0, len(arr)
    while low < high:
        mid = (low+high) // 2 # low + (high-low)//2 if cares about overflow
        if target < arr[mid]:
            high = mid
        elif target > arr[mid]:
            low = mid + 1
        else:
            return mid
    return -1
```


This simple case is mostly useful to check if a target value is in a sorted array, for example [the binary_search function in C++ Standard library](https://cplusplus.com/reference/algorithm/binary_search/).

For example, the result should be 2 in the test case below:

```python
arr = [5, 6, 7, 9]
target = 7
```

![Basic Format](https://miro.medium.com/v2/resize:fit:828/format:webp/1*2-CTbK95XtbbyWg_xUqfYQ.png)


# 2. [Bisect_left](https://docs.python.org/3/library/bisect.html)

Given a **sorted** array of integers and a target integer, return the index of the first element **equals** to target, or the **insert position** of the target if no equal element exists.

```python
def bisect_left(arr, target):
    low, high = 0, len(arr)
    while low < high:
        mid = (low+high)//2
        if target > arr[mid]:
            low = mid+1
        else:
            high = mid
    return low
```

This algorithm has two relaxed conditions comparing to the basic format:

* Allow duplicates in the array, instead of being unique
* Return the insert position if the target does not exists, instead of a sentinel value -1

For example, the result should be 2 in the test case below:

```python
arr = [5,6,7,7,9]
target = 7
```

![Bisect Left](https://miro.medium.com/v2/resize:fit:964/format:webp/1*FcGnpD8zqgv7Ek6qd7YzaQ.png)

The trick of bisect_left is the loop invariant `low` . All elements on the left side of `low` are strictly less than `target` . So when the loop exits, element at `low` is the first element greater or equal to `target` . `low` is also the `rank` of target in the array.

**This is the most commonly used binary_search algorithm.**

3. [bisect_right](https://docs.python.org/3/library/bisect.html)

Given a **sorted** array of integers and a target integer, return the index of the **last** insert position of target.

```python
def bisect_right(arr, target):
    low, high = 0, len(arr)
    while low < high:
        mid = (low+high)//2
        if target < arr[mid]:
            high = mid
        else:
            low = mid+1
    return high
```

This algorithm essentially returns the index of the first element strictly larger than target. For example, the result should be 4 in the test case below:
```python
arr = [5,6,7,7,9]
target = 7
```

![Bisect Right](https://miro.medium.com/v2/resize:fit:1008/format:webp/1*XQxV0HzgBkkZjrMDNxb-5w.png)

The trick of bisect_right is the loop invariant `high`. Elements at and to the right of `high` are strictly larger than target .

----

For an iterative implementation of binary search, the time complexity is O(lgN) and space is O(1), where N is the length of the array.

For a recursion implementation, left as an exercise to the reader, the time complexity is O(lgN) but space is O(lgN) due to stack of function calls.

_Q.E.D._

References:

[https://en.wikipedia.org/wiki/Binary_search_algorithm](https://en.wikipedia.org/wiki/Binary_search_algorithm)
[https://docs.python.org/3/library/bisect.html](https://docs.python.org/3/library/bisect.html)
[http://www.cplusplus.com/reference/algorithm/binary_search/](http://www.cplusplus.com/reference/algorithm/binary_search/)

----

Originally posted at [https://levelup.gitconnected.com/practical-algorithms-tier-0-binary-search-99508cc62fe4](https://levelup.gitconnected.com/practical-algorithms-tier-0-binary-search-99508cc62fe4)
