---
layout: post
author: Yan
title: Fenwick Tree
---

I recently encountered a problem that can be solved efficiently with _Fenwich Tree_, aka _Binary Indexed Tree_. This is the notes about how to explain the algorithm to myself.

## Section 1. The (simplified) problem example and manual solution.

**Step 1.** The problem: Given an input array, `nums = [1004, 1009, 1006, 1001, 1002, 1005, 1003, 9999]`, how to efficiently do sum for any ranges, if element updates allowed?

**Step 2.** To sum up the first `7` elements, we do (in _Python_) `total = sum(nums[0:7])`, or verbosely `total = nums[0] + nums[1] + nums[2] + nums[3] + nums[4] + nums[5] + nums[6]`. Notation `[0:7]` in Python means range from 0 to 6, equivalent to the math close-open notation `[0, 7)`. Why `7`? Because it is complex enough to demonstrate the thinking process, yet simple enough to manually iterate through.

**Step 3.** Pause a bit and think about the number `7`. It can be expressed as `4 + 2 + 1`, and that's exactly the binary representation `b111 = b100 + b010 + b001`

**Step 4.** Similarly, the range `[0:7]` can break into groups as `[0:4]+[4:6]+[6:7]`. Or explicitly `total = (nums[0] + nums[1] + nums[2] + nums[3]) + (nums[4] + nums[5]) + (nums[6])`, where counts of elements coincide with the _binary_ representation of the number `7`.

**Step 5.** We can build an `aux` array to store the partial sums needed in Step 4, such that `total = aux[4] + aux[6] + aux[7]`. Here both `nums` and `aux` are 0-indexed arrays, for the clarity of implementations in practice, instead of mathematical beautifulness with 1-indexed arrays. Obviously:

```python
aux[4] = nums[0]+nums[1]+nums[2]+nums[3]
aux[6] = nums[4]+nums[5]
aux[7] = nums[6]
```

![3 aux elements are used to calculate [0:7]](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*JQ6qszGZP2nh0hXg)

**Step 6.** Now again examine the number `7`, and relate the indices of aux used in Step 5, which are `7`, `6` and `4`, or `b111`, `b110` and `b100` in binary representation. This is where the _Binary Indexed_ in the name of the algorithm is from. Now we found the sum/query method. Given an index number (7) to sum up to, the indices of the `aux` array are: the number itself (7 or b111), chop off the last 1 in the previous number (6 or b110), and chop off the last 1 in the previous number (4 or b100), and chop off the last 1 again gives 0 so we stop.

**Step 7.** Now we can fill all `aux` elements, with ranges of `nums`. Note that `aux[i]` is determined by its start position and length in `nums`:
* Start: `i-1`. For example, `aux[6]` starts at `5` in `nums`
* Length: the value of last set bit. For example, `aux[6]` has length of `2`, because `6==b110` and the value of the last set bit is `b10==2`.

![The aux-nums mapping](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*7llPEXQtiU5x9Z7sAtRgyw.png)


## Section 2. The algorithm

**Step 1.** The `query_sum` function (assume we already have `aux` built). Given an index i, find the sum of range `[0:i]`. For a number `i`, the trick to chop off the last 1 (called the _last set bit_) is `i-(i&-i)`. The query takes `O(logN)` time, because the tree depth is bound by `logN`. That's why there is Tree in the name of this algorithm.

```python
def query_sum(self, i):
        res = 0
        while i > 0:
            res += self.aux[i]
            i -= i & -i
        return res

```

**Step 2.** The _update_ function (assume we already have `aux` built). Given an index `i` for `nums`, and a new `value`, update `aux`. The tricky part is, how to find all elements in `aux` that are affected by the change of `nums[i]`. Obviously `aux[j]` where `j=i+1` is always affected. Then `j+j&-j` recursively until `j` is out of bound of `aux`, which can be observed if we reverse the aux-nums mapping above, to a nums-aux mapping (note to self: need more thinking here). The update takes `O(lgN)` time, as it's also [bounded by the depth of the tree](https://www.geeksforgeeks.org/dsa/binary-indexed-tree-or-fenwick-tree-2/).

![The nums-aux mapping](https://miro.medium.com/v2/resize:fit:1034/format:webp/0*x3lrI85xG3M7Na3R)

```python
def update(self, i, value):
        diff = value - self.nums[i]
        self.nums[i] = value
        i += 1
        while i < len(self.nums)+1:
            self.aux[i] += diff
            i += i & -i
```

**Step 3.** Build `aux`. Simply iterate through `nums` and call `update` on the index `i`.
```python
def __init__(self, nums):
        self.nums = [0] * len(nums)
        self.aux = [0] * (len(nums) + 1)
        for i, v in enumerate(nums):
            self.update(i, v)
```


_Q.E.D._

[Source code and tests](https://github.com/runtimee/proto3/blob/129b923/misc/fenwich.py)

References:
[https://www.hackerearth.com/practice/data-structures/advanced-data-structures/fenwick-binary-indexed-trees/tutorial/](https://www.hackerearth.com/practice/data-structures/advanced-data-structures/fenwick-binary-indexed-trees/tutorial/)
[https://www.geeksforgeeks.org/dsa/binary-indexed-tree-or-fenwick-tree-2/](https://www.geeksforgeeks.org/dsa/binary-indexed-tree-or-fenwick-tree-2/)

----

Originally published at [http://runtimee.wordpress.com](https://runtimee.wordpress.com/2019/11/14/fenwick-tree/) on November 14, 2019.
Also reposted at [https://medium.com/@runtimee/fenwick-tree-f26fe45855a8](https://medium.com/@runtimee/fenwick-tree-f26fe45855a8)
