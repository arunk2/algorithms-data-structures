## Coin Exchange Problem:
Coin exchange problem is nothing but finding the minimum number of coins (of certain denominations) that add up to a given amount of money. It is a knapsack type problem.

The interesting fact is that it has 2 variations:

### Greedy Algorithm:
For some type of coin system (canonical coin systems - like the one used in the India, US and many other countries) a greedy approach works.
The valued coins will be like { 1, 2, 5, 10, 20, 50, 100, 500, 1000}.
i.e. In our algorithm we always choose the biggest denomination, subtract the all possible values and going to the next denomination.


```
# Denominations of Indian Currency
deno = [1, 2, 5, 10, 20, 50, 100, 500, 1000]
n = len(deno)
 
def findMin(int V)
    ans = []

    i = n-1	
    while (i>=0):
        while (V >= deno[i]):
           V = V - deno[i]
           ans.append(deno[i])

    for coin in ans:
	print coin

V = 93
findMin(V)
```

### Dynamic programming:
The above solution wont work good for any arbitrary coin systems.
For example: if the coin denominations were 1, 3 and 4.
To make 6, 

the greedy algorithm would choose three coins (4,1,1), whereas the optimal solution is two coins (3,3)


Hence, we need to check all possible combinations.
But this problem has 2 property of the Dynamic Programming.
1. Optimal Substructure
To count total number solutions, we can divide all set solutions in two sets.
a) Solutions that do not contain mth coin (or Sm).
b) Solutions that contain at least one Sm.
Let count(S[], m, n) be the function to count the number of solutions, then it can be written as sum of count(S[], m-1, n) and count(S[], m, n-Sm).


```
count( S, m, n ) =

	Base condition:
	if (n = 0)           => 1
	if (n < 0)           => 0
	if (m <=0 && n >= 1) => 0
	 
	Recurrence relation:
	count( S, m - 1, n ) + count( S, m, n-S[m-1] )
```

2. Overlapping Subproblems
If we go for a naive recursive implementation of the above,  We repreatedly calculate same subproblems. 


Hence, a suitable candidate for the DP. Following is the DP implementation

```
# Dynamic Programming Python implementation of Coin Change problem
def count(S, m, n):
    # We need n+1 rows as the table is consturcted in bottom up
    # manner using the base case 0 value case (n = 0)
    table = [[0 for x in range(m)] for x in range(n+1)]
 
    # Fill the enteries for 0 value case (n = 0)
    for i in range(m):
        table[0][i] = 1
 
    # Fill rest of the table enteries in bottom up manner
    for i in range(1, n+1):
        for j in range(m):
            # Count of solutions including S[j]
            x = table[i - S[j]][j] if i-S[j] >= 0 else 0
 
            # Count of solutions excluding S[j]
            y = table[i][j-1] if j >= 1 else 0
 
            # total count
            table[i][j] = x + y
 
    return table[n][m-1]
 
# Driver program to test above function
arr = [1, 2, 3]
m = len(arr)
n = 4
print(count(arr, m, n))
```
