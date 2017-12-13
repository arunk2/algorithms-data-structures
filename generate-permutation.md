## Generate permutations
To print all the permutations of a give array.
For example, the array [A,B,C]

should print
```
ABC
ACB
BAC
BCA
CBA
CAB
```

Working python code based on back tracing

```
def permute(a, l, r):
    if l==r:
        print ''.join(a)
    else:
        for i in xrange(l,r+1):
            a[l], a[i] = a[i], a[l]
            permute(a, l+1, r)
            a[l], a[i] = a[i], a[l] # backtrack
 
arr = ['A','B','C']
permute(a, 0, len(arr)-1)
```
