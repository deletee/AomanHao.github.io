---
title: leetcode题解
date: 2018-08-16 09:39:40
tags: [笔面试]
toc: true
---

leetcode 高频

<!--more-->

### 三数之和

给定一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？找出所有满足条件且不重复的三元组。

注意：答案中不可以包含重复的三元组。

例如, 给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]

### 1	Two Sum	
5	array、set	sort、Two Pointers
### 8	String to Integer (atoi)	5	string	Math
### 15	3Sum	5	array	Two Pointers
### 20	Valid Parentheses	5	string	Stack
### 21	Merge Two Sorted Lists	5	linked list	sort、Two Pointers、merge
### 28	Implement strStr()	5	string	Two Pointers、KMP、rolling hash
### 50	Pow(x, n)	5	 	Binary Search、Math
### 56	Merge Intervals	5	array、linked list、red-black tree	sort、merge
### 57	Insert Interval	5	array	sort
### 65	Valid Number	5	string	Math
### 70	Climbing Stairs	5	 	DP
### 73	Set Matrix Zeroes	5	array	 
### 88	Merge Sorted Array	5	array	Two Pointers、merge
### 98	Validate Binary Search Tree	5	tree	DFS
### 125	Valid Palindrome	5	string	Two Pointers
### 127	Word Ladder	5	graph	BFS、path
### 2	Add Two Numbers	4	linked list	Two Pointers、Math
### 12	Integer to Roman	4	 	Math
### 13	Roman to Integer	4	 	Math
### 22	Generate Parentheses	4	string	DFS
### 23	Merge k Sorted Lists	4	linked list、heap	sort、Two Pointersmerge
24	Swap Nodes in Pairs	4	linked list	 
27	Remove Element	4	array	Two Pointers
46	Permutations	4	array	permutation
49	Anagrams	4	string、hashtable	 
67	Add Binary	4	string	Two Pointers、Math
69	Sqrt(x)	4	 	Binary Search
77	Combinations	4	 	combination
78	Subsets	4	array	Recursion、combination
79	Word Search	4	array	DFS
91	Decode Ways	4	string	Recursion、DP
102	Binary Tree Level Order Traversal	4	tree	BFS
129	Sum Root to Leaf Numbers	4	tree	DFS
131	Palindrome Partitioning	4	string	DFS
4	Median of Two Sorted Arrays	3	array	Binary Search
7	Reverse Integer	3	 	Math
10	Regular Expression Matching	3	string	Recursion、DP
17	Letter Combinations of a Phone Number	3	string	DFS
19	Remove Nth Node From End of List	3	linked list	Two Pointers
26	Remove Duplicates from Sorted Array	3	array	Two Pointers
29	Divide Two Integers	3	 	Binary Search
33	Search in Rotated Sorted Array	3	array	Binary Search
34	Search for a Range	3	array	Binary Search
39	Combination Sum	3	array	combination
43	Multiply Strings	3	string	Two Pointers、Math
44	Wildcard Matching	3	string	Recursion、DP、greedy
51	N-Queens	3	array	DFS
52	N-Queens II	3	array	DFS
53	Maximum Subarray	3	array	DP
62	Unique Paths	3	array	DP
63	Unique Paths II	3	array	DP
64	Minimum Path Sum	3	array	DP
72	Edit Distance	3	string	DP
74	Search a 2D Matrix	3	array	Binary Search
81	Search in Rotated Sorted Array II	3	array	Binary Search
82	Remove Duplicates from Sorted List II	3	linked list	Recursion、Two Pointers
83	Remove Duplicates from Sorted List	3	linked list	 
86	Partition List	3	linked list	Two Pointers
93	Restore IP Addresses	3	string	DFS
94	Binary Tree Inorder Traversal	3	tree、hashtable	Recursion、morris、Stack
103	Binary Tree Zigzag Level Order Traversal	3	queue、tree	BFS、Stack
105	Construct Binary Tree from Preorder and Inorder Tr	3	array、tree	DFS
106	Construct Binary Tree from Inorder and Postorder T	3	array、tree	DFS
108	Convert Sorted Array to Binary Search Tree	3	tree	DFS
109	Convert Sorted List to Binary Search Tree	3	linked list	Recursion、Two Pointers
112	Path Sum	3	tree	DFS
114	Flatten Binary Tree to Linked List	3	tree	Recursion、Stack
116	Populating Next Right Pointers in Each Node	3	tree	DFS
128	Longest Consecutive Sequence	3	array	 
130	Surrounded Regions	3	array	BFS、DFS
132	Palindrome Partitioning II	3	string	DP
3	Longest Substring Without Repeating Characters	2	string、hashtable	Two Pointers
5	Longest Palindromic Substring	2	string	 
9	Palindrome Number	2	 	Math
11	Container With Most Water	2	array	Two Pointers
18	4Sum	2	array	 
25	Reverse Nodes in k-Group	2	linked list	Recursion、Two Pointers
31	Next Permutation	2	array	permutation
35	Search Insert Position	2	array	 
36	Valid Sudoku	2	array	 
37	Sudoku Solver	2	array	DFS
38	Count and Say	2	string	Two Pointers
40	Combination Sum II	2	array	combination
41	First Missing Positive	2	array	sort
42	Trapping Rain Water	2	array	Two Pointers、Stack
45	Jump Game II	2	array	 
47	Permutations II	2	array	permutation
48	Rotate Image	2	array	 
54	Spiral Matrix	2	array	 
55	Jump Game	2	array	 
59	Spiral Matrix II	2	array	 
61	Rotate List	2	linked list	Two Pointers
66	Plus One	2	array	Math
68	Text Justification	2	string	 
75	Sort Colors	2	array	sort、Two Pointers
76	Minimum Window Substring	2	string	Two Pointers
80	Remove Duplicates from Sorted Array II	2	array	Two Pointers
84	Largest Rectangle in Histogram	2	array	Stack
87	Scramble String	2	string	Recursion、DP
89	Gray Code	2	 	combination
90	Subsets II	2	array	Recursion、combination
92	Reverse Linked List II	2	linked list	Two Pointers
97	Interleaving String	2	string	Recursion、DP
99	Recover Binary Search Tree	2	tree	DFS
101	Symmetric Tree	2	tree	DFS
110	Balanced Binary Tree	2	tree	DFS
113	Path Sum II	2	tree	DFS
115	Distinct Subsequences	2	string	DP
117	Populating Next Right Pointers in Each Node II	2	tree	DFS
124	Binary Tree Maximum Path Sum	2	tree	DFS
6	ZigZag Conversion	1	string	 
14	Longest Common Prefix	1	string	 
16	3Sum Closest	1	array	Two Pointers
30	Substring with Concatenation of All Words	1	string	Two Pointers
32	Longest Valid Parentheses	1	string	DP
58	Length of Last Word	1	string	 
60	Permutation Sequence	1	 	permutation、Math
71	Simplify Path	1	string	Stack
85	Maximal Rectangle	1	array	DP、Stack
95	Unique Binary Search Trees II	1	tree	DP、DFS
96	Unique Binary Search Trees	1	tree	DP
100	Same Tree	1	tree	DFS
104	Maximum Depth of Binary Tree	1	tree	DFS
107	Binary Tree Level Order Traversal II	1	tree	BFS
111	Minimum Depth of Binary Tree	1	tree	DFS
118	Pascal’s Triangle	1	array	 
119	Pascal’s Triangle II	1	array	 
120	Triangle	1	array	DP
121	Best Time to Buy and Sell Stock	1	array	DP
122	Best Time to Buy and Sell Stock II	1	array	greedy
123	Best Time to Buy and Sell Stock III	1	array	DP
126	Word Ladder II	1
