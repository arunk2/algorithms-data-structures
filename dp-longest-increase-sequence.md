```
global max_lis_length # stores the final LIS

def lis(arr, n):
	global max_lis_length
	# Base Case
	if n == 1:
		return 1

	current_lis_length = 1

	for i in xrange(0, n-1):
		subproblem_lis_length = lis(arr, i)

		if arr[i] < arr[i+1] and current_lis_length < (subproblem_lis_length+1):
			current_lis_length = (subproblem_lis_length+1)

	if (max_lis_length < current_lis_length):
		max_lis_length = current_lis_length

	return current_lis_length



def lis_tabulation(arr, n):
 
    # Declare the list (array) for LIS and initialize LIS
    # values for all indexes
    lis = [1]*n


    for i in range (1, n):
    	for j in range (0, i):
    		if arr[i] > arr[j] and lis[i] < (lis[j]+1):
    			lis[i] = lis[j]+1
 
    # Initialize maximum to 0 to get the maximum of all
    # LIS
    maximum = 0
 
    # Pick maximum of all LIS values
    for i in range(n):
        maximum = max(maximum , lis[i])
 
    return maximum



# Driver program to test the functions above
def main():
	global max_lis_length
	max_lis_length = 1
	arr = [10, 22, 9, 33, 21, 50, 41, 60]
	n = len(arr)
	print "Length of LIS is", lis(arr, n)
	print "Length of LIS is", lis_tabulation(arr, n)

if __name__=="__main__":
	main()
```
