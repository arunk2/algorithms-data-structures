## Generate valid parenthesis:
Generate all combinations of well-formed parentheses.

For example, n = 3, should print set of 

"((()))", "(()())", "(())()", "()(())", "()()()"

### Working code:
```
def generateParenthesis(result, current, open, close):
        if open == 0 and close == 0:
            result.append(current)
        if open > 0:
            generateParenthesis(result, current + "(", open - 1, close)
        if open < close:
            generateParenthesis(result, current + ")", open, close - 1)

generateParenthesis([], '', 3, 3)

```


    
