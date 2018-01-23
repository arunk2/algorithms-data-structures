## Generating all combinations
Sometime we need to generate all combinations of 1 element from each list, from a give list of lists.

### For example
```
Input:
      ['A', 'B'], 
      ['1', '2']
      
Output:
      'A 1', 
      'A 2', 
      'B 1', 
      'B 2'

```

### Working python code 
```
def generateCombinations(words_words, depth, size, sentence):
    if depth == size:
        print ''.join(sentence)
        return
    
    cur_sent_back = sentence[:]
    for words in words_words[depth]:
        cur_sent = cur_sent_back[:]
        cur_sent.append(words)
        generateCombinations(words_words, depth+1, size, cur_sent)
    
    return None
    
    
if __name__ == '__main__':
    words = [['A', 'B', 'C'],
             ['1', '2', '3', '4'],
             ['a', 'b']]
             
    generateCombinations(words, 0, len(words), [])
    print 'Generation completed!'
    
```
