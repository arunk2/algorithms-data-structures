## Generate combinations
For the Input list [1, 2, 3, 4, 5] with k = 3, to generate output
```
    [1, 2, 3]
    [1, 2, 4]
    [1, 2, 5]
    [1, 3, 4]
    [1, 3, 5]
    [1, 4, 5]
    [2, 3, 4]
    [2, 3, 5]
    [2, 4, 5]
    [3, 4, 5]
```
The working python code

```
def my_combinations(items, k, out):
    if k==0:
        print out
        return

    for i in range(len(items)):
        new_out = out[:]
        new_out.append(items[i])
        my_combinations(items[i+1:], k-1, new_out)
````
