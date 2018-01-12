## Subsetsum Problem:
Given a set of non-negative integers, and a value sum, determine the subset of the given set with sum equal to given sum.
Thought of implementing problem, as I dont see any implementation printing all the valid subsets.

```
def subsetsum(arr, i, sum, ss):
    if i >= len(arr):
        if sum == 0:
            print ss
            return 1
        else:
            return 0
 
    ss1 = ss[:]
    count = subsetsum(arr, i + 1, sum, ss1)
    ss1.append(arr[i])
    count += subsetsum(arr, i + 1, sum - arr[i], ss1)
    return count

arr = [1, 2, 3, 10, 5, 7]
sum = 14
a = []
print subsetsum(arr, 0, sum, a)
```
