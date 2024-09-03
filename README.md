# Trie


A Trie (pronounced "try") is a tree-like data structure that is used to store a dynamic set of strings where the keys are usually strings. The name "Trie" comes from the word "retrieval", as it is designed to retrieve keys in a dataset quickly.

Each node in a Trie represents a single character from a string.
The root node represents an empty string.
Each edge in the Trie represents a connection between characters.
A path from the root to a node represents a prefix of the stored string.
A complete string is represented by a path from the root to a node that is marked as an end-of-word.


Insert Operation:
To insert a string S of length n, start from the root.
For each character S[i] in the string:
If the current node has a child corresponding to S[i], move to that child.
If not, create a new child node corresponding to S[i] and move to that node.
After inserting all characters, mark the last node as an end-of-word node.

Search Operation:
To search for a string S in the Trie, start from the root.
For each character S[i]:
If the current node has a child corresponding to S[i], move to that child.
If not, the string S is not present in the Trie.
If you reach the end of S and the last node is marked as an end-of-word, the string S is present in the Trie.

Starts-With Operation:
This operation checks if there is any string in the Trie that starts with a given prefix P.
Follow the same steps as the search operation, but instead of checking for the end-of-word, return true if you can traverse the entire prefix P.

Delete Operation:
Deletion in a Trie is more complex. It involves traversing the string to the end node and then:
Unmark the end-of-word flag.
If the node has no children, it can be safely deleted.
This may propagate backward, removing nodes that are no longer part of any string.


Let:
T be the Trie.
S be a string of length n.
root be the root node of the Trie.
node be the current node being examined.
children(node) be the set of children nodes of node.
char(i) be the i-th character of string S.


Insert(T, S):
  node = root
  for i = 0 to n-1:
    if char(i) not in children(node):
      create a new node for char(i)
    node = children(node)[char(i)]
  mark node as end-of-word


Search(T, S):
  node = root
  for i = 0 to n-1:
    if char(i) not in children(node):
      return False
    node = children(node)[char(i)]
  return node is end-of-word
Starts-With Operation:
Starts-With(T, P):
  node = root
  for i = 0 to m-1:
    if char(i) not in children(node):
      return False
    node = children(node)[char(i)]
  return True


Delete(T, S):
  _delete(node, S, depth):
    if node is None:
      return False
    if depth == len(S):
      if node is end-of-word:
        unmark end-of-word
      return len(children(node)) == 0
    char = S[depth]
    if _delete(children(node)[char], S, depth + 1):
      delete children(node)[char]
      return len(children(node)) == 0
    return False
  _delete(root, S, 0)
  

Insert: The time complexity is O(n) where n is the length of the string being inserted.
Search: The time complexity is O(n) where n is the length of the string being searched.
Starts-With: The time complexity is O(m) where m is the length of the prefix.
Delete: The time complexity is O(n) where n is the length of the string being deleted.

