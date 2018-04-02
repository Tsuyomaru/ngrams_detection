# ngrams_detection
Project made for "Software Development for Computational Systems" class, fall semester 2017-2018, di-uoa (NKUA) <br>
Based on the Sigmod Contest 2017

## Description
The goal of the project is the detection of n-grams (sequences of N number of words) in blocks of text.

## Trie Structure
A Trie Structure was use to make the search process more efficient, which is a tree like structure with each node being a word of the n-gram. Therefore each n-gram is a child of the trie's root. A node is marked as final if it contains the last word of an n-gram. As a result, all the leaf nodes and some of the middle ones are considered to be final nodes.
```
The n-grams "this is a" and "this is a cat" would be represented in the trie structure with the same nodes for
the "this is a" part. 
 -> The "this" node is a child of the root. 
 -> The "a" and "cat" nodes are marked as finals.
```
The Trie struct contains only the root of the structure, with extra fields being added on later versions of the project. <br><br>
The structure can complete 3 tasks:
* Add N-gram (A)
* Delete N-gram (D)
* Search N-grams in text (Q)
* Top-K Ngrams (F) (Only used with the Tok-K functionality on [Part 2](part2) and [Part 3](part3) of the project)
### Add Task
This task configures the trie structure to add a new n-gram. If the n-gram exists already, the structure remains unaltered. This task does not produce any exit or output to the screen. <br>
Instruction: A n-gram
### Delete Task
This task configures the trie structure to remove a requested n-gram. If the n-gram does not exist, it remains unaltered. If the n-gram exists, its nodes are deleted. If each nodes are used as part of another, they remain in the structure but their connection to requested n-gram is severed. This task does not produce any exit or output to the screen. <br>
Instruction: D n-gram
### Query or Search Task
This task searches for all the appearing n-grams in a block of text. Its result is a line with all the appearing n-grams, in order of appearance, separated by the "|" character. If no n-gram is found, a "-1" is printed instead. <br>
Instruction: Q block_of_text
### F Signifier
The F instruction signifies the end of a batch of A, D and Q instructions. At the first version of the project it has no functional value. However it is later used for a Top-K query of the most common results in the queries of one batch.

## [Part 1](part1)
### Trie Node
Each node represents a word of an n-gram. The structure contains the word, either by array or pointer depending the version of the trie node, an array of children trie nodes, the following word on an n-gram, the size of the array, the occupied number of slots on the array and a flag which turns true when the node is a final node of an n-gram. <br>
A binary search algorithm is used when searching the children array since the children nodes are stored alphabetically. <br>
The differences between the three versions of the trie nodes are:
* trie_node: The word is stored in an allocated space and is accessed by a pointer
* semistatic_trie_node: Most words (less than 30 characters) are stored in an array and the rest on an allocated space. It is accessed by a pointer which points accordingly to where the word is stored.
* semistatic_trie_node_v2: Most words (less than 30 characters) are stored in an array and the rest on an allocated space. The word is accessed by checking where the word actually resides and using the correct variable.

### Binary Heap
A Binary Heap was used in conjuction with the Trie Structure for the query task. It stores the n-grams found in text. Before an n-gram is added to the printed results, it is looked up in the Binary Heap so as not to be printed twice. The Binary Heap is cleared after every Q task. 

### File I/O
In order to initialize the structure and to execute the necessary tasks, two files are needed. The initFile contains only A tasks, each one separated by a new line, and it is used to initialize the Trie Structure. The queryFile contains any number of A, D, Q and F instructions, each one separeted by a new line. These are executed serially so each query is answered by up to date version of the Trie at the time. <br>
Both of these files go through a parser to determine which type of task must be executed. What follows the instruction, be it n-gram of text, goes through a tokenizer which returns an array of the words in the same order and it used by the Trie's functions. 

<!--
## [Part 2](part2)
### Trie Node
The functionality of the Trie and its nodes is advanced and separated into two parts, a dynamic and a static. The dynamic Trie uses the nodes of the previous part without any changes in its structure and functionality. The static nodes were written with the semistatic_node as a base, which was the most efficient of the three dynamic nodes of Part 1. There are two main differences between the two types of Tries, one functional and one structural. The functional difference is that the trie is finalized after its initialization and the workload is guaranteed to not have addition and deletion tasks.  The only available tasks for the workload are search and Top-K queries. The structural difference is that when having nodes with a single child, the word of the parent node and its child are saved in a single node instead of having long chains of single nodes. This is achieved with the addition of a shrink function to the Trie which is called after the initialization and its duty is to go through the structure, to detect all the single child nodes and compress them without losing any valuable information such as the final signifier of a node or ngram. Obviously, this changes the structure of the nodes and the internal functionality but little change is necessary on the Trie and its functions. Moreover the Trie Node Connector minimizes these changes, as it will be made clear in the trie_node_connector structure description below. <br>
The static nodes contain the same variables as in the semistatic_node structure but instead of a boolean to represent a final node, two new variables are used. These two variables are a short integer array that saved the length of the word(s) in the node with the length's sign representing the final node, and a short integer for the size of the array or the number of words saved in a static node. <br>
There are two versions of the static node with small differences:
* static_trie_node_semi: The lengths array is always dynamically allocated
* static_trie_node_semi_improved: The lengths array has a static version with a size of LENGTH. This LENGTH is calculated by dividing the size of the word array with the mean of the average size of English words encountered in texts and the average size of English words on a dictionary. If the words saved in one node are more than the calculated LENGTH, then the array is dynamically allocated. Both versions of the array can be accessed by the same pointer as do words in this node structure and both the semistatic_trie_node and static_trie_node_semi.

### Trie Node Connector


### Treap


### Bloom Filter


### Linear Hash


## [Part 3](part3)
-->

## Authors
* [dexter957](https://github.com/dexter957)
* [Tsuyomaru](https://github.com/tsuyomaru)
