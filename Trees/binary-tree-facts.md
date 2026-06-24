## Pre Binary Tree situations
Prior to invention of Binary Tree, Linear DS like arrays, Linked list were filling its shoes.
Problem these had is speed of deletions and insertions.
LinkedLists offer faster insertions and slower deletions but edged away by array over slower access to elements.
Arrays edges over linked lists in fast access to element O(1) and lags in deletion O(n).

## Rise of Binary Tree
Neither structures excelled at access time, insertions, deletions
This bridges gap between arrays an linkedlists
Search time reduced from O(n) to O(logn).

## Types Tree
Binary Search Tree --> smaller vals go left, larger vals go right.
AVL Tree --> a breakthrough, first self balancing Tree. It introduces concept of balance factor.
B Tree --> breakthrough, leading to under the hood scenes of database storage. B+ trees are advanced versions of B tree. primarily used in databases.
Red Black Tree.

## facts
Real world objects have hierarchy
Tree data structure offers hierarchy based storing objects
Even html docs are hierarchy based, storage devices hierarchy based.
A tree node itself does not contain its children, but it references those children. tree node contains its own value and references of its children but not actual children.
A child does not know its own parent, but parent know its children
A child cannot have more than one parent, but parent can have more than one children.
A tree with one child result this structure to single LL
Tree node with one children is called skewed tree.
