## Trie Data structure:
According to wikipedia: In computer science, a trie, or prefix tree, is an ordered tree data structure that is used to store an associative array where the keys are usually strings. Unlike a binary search tree, no node in the tree stores the key associated with that node; instead, its position in the tree shows what key it is associated with. All the descendants of a node have a common prefix of the string associated with that node, and the root is associated with the empty string. Values are normally not associated with every node, only with leaves and some inner nodes that correspond to keys of interest.


### Simple implementation in python
```
class Trie:
  def __init__(self):
     word_end = '_end_'
     root = {}
     
  def add_word(self, word):
     self.add_words([word])
 
  def add_words(self, words):
     for word in words:
         current_dict = self.root
         for letter in word:
             current_dict = current_dict.setdefault(letter, {})
         current_dict[word_end] = word_end

 
  def check_word(self, word):
     current_dict = self.root
     for letter in word:
         if letter in current_dict:
             current_dict = current_dict[letter]
         else:
             return False
     else:
         if _end in current_dict:
             return True
         else:
             return False



tree = Trie()
tree.add_word('foo', 'bar', 'baz', 'barz')
print tree
"""
{'b': {'a': {'r': {'_end_': '_end_', 'z': {'_end_': '_end_'}}, 
             'z': {'_end_': '_end_'}}}, 
 'f': {'o': {'o': {'_end_': '_end_'}}}}
 """
 
print check_word('baz')
# True
print check_word('barz')
# True
print check_worf('barzz')
# False
```
