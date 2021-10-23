![picture 1](https://i.loli.net/2021/09/25/Xrd3OM9Ltf8NRFP.png)  

- 什么时候用dijkstra？每个点的边权不一样

 
- 搜索的本质是枚举 
- 当我们不知道循环次数时，会用到递归枚举


- step 1: 初始化
  - 把初始节点放到queue里，如果有多个就都放进去
  - 并标记初始节点的距离为0，记录在distance的hashmap里
  - distance有两个作用，一个是判断是否已经访问过，而是记录离起点距离

- step 2: 不断访问队列
  - while循环 + 每次pop队列中的一个点出来

- step 3： generate相邻节点
  - popo出的节点的相邻节点，加入队列并在distance中存储距离


- BFS记录的是节点在搜索树上的最小深度
- 187 problems

|   | # | Title | Acceptance | Difficulty | Frequency |
| --- | --- | --- | --- | --- | --- |
|  | 100 | Same Tree | 54.9% | Easy |  |
|  | 101 | Symmetric Tree | 50.1% | Easy |  |
|  | 102 | Binary Tree Level Order Traversal | 59.1% | Medium |  |
|  | 103 | Binary Tree Zigzag Level Order Traversal | 52.0% | Medium |  |
|  | 104 | Maximum Depth of Binary Tree | 70.1% | Easy |  |
|  | 107 | Binary Tree Level Order Traversal II | 57.1% | Medium |  |
|  | 111 | Minimum Depth of Binary Tree | 41.3% | Easy |  |
|  | 116 | Populating Next Right Pointers in Each Node | 52.9% | Medium |  |
|  | 117 | Populating Next Right Pointers in Each Node II | 44.4% | Medium |  |
|  | 126 | Word Ladder II | 25.8% | Hard |  |
|  | 127 | Word Ladder | 33.7% | Hard |  |
|  | 130 | Surrounded Regions | 31.6% | Medium |  |
|  | 133 | Clone Graph | 43.2% | Medium |  |
|  | 199 | Binary Tree Right Side View | 58.1% | Medium |  |
|  | 200 | Number of Islands | 51.9% | Medium |  |
|  | 207 | Course Schedule | 44.7% | Medium |  |
|  | 210 | Course Schedule II | 44.8% | Medium |  |
|  | 226 | Invert Binary Tree | 69.4% | Easy |  |
|  | 261 | Graph Valid Tree | 44.6% | Medium |  |
|  | 269 | Alien Dictionary | 34.3% | Hard |  |
|  | 279 | Perfect Squares | 51.0% | Medium |  |
|  | 286 | Walls and Gates | 57.7% | Medium |  |
|  | 297 | Serialize and Deserialize Binary Tree | 52.1% | Hard |  |
|  | 301 | Remove Invalid Parentheses | 45.9% | Hard |  |
|  | 302 | Smallest Rectangle Enclosing Black Pixels | 54.5% | Hard |  |
|  | 310 | Minimum Height Trees | 36.0% | Medium |  |
|  | 314 | Binary Tree Vertical Order Traversal | 49.0% | Medium |  |
|  | 317 | Shortest Distance from All Buildings | 43.7% | Hard |  |
|  | 322 | Coin Change | 38.9% | Medium |  |
|  | 323 | Number of Connected Components in an Undirected Graph | 59.7% | Medium |  |
|  | 329 | Longest Increasing Path in a Matrix | 48.2% | Hard |  |
|  | 339 | Nested List Weight Sum | 78.4% | Medium |  |
|  | 364 | Nested List Weight Sum II | 66.0% | Medium |  |
|  | 365 | Water and Jug Problem | 32.9% | Medium |  |
|  | 399 | Evaluate Division | 55.9% | Medium |  |
|  | 404 | Sum of Left Leaves | 53.2% | Easy |  |
|  | 407 | Trapping Rain Water II | 45.8% | Hard |  |
|  | 417 | Pacific Atlantic Water Flow | 46.4% | Medium |  |
|  | 433 | Minimum Genetic Mutation | 44.8% | Medium |  |
|  | 449 | Serialize and Deserialize BST | 55.3% | Medium |  |
|  | 463 | Island Perimeter | 68.3% | Easy |  |
|  | 490 | The Maze | 53.9% | Medium |  |
|  | 499 | The Maze III | 43.9% | Hard |  |
|  | 505 | The Maze II | 50.3% | Medium |  |
|  | 513 | Find Bottom Left Tree Value | 64.0% | Medium |  |
|  | 514 | Freedom Trail | 45.6% | Hard |  |
|  | 515 | Find Largest Value in Each Tree Row | 63.6% | Medium |  |
|  | 529 | Minesweeper | 63.3% | Medium |  |
|  | 530 | Minimum Absolute Difference in BST | 55.7% | Easy |  |
|  | 542 | 01 Matrix | 43.1% | Medium |  |
|  | 547 | Number of Provinces | 62.1% | Medium |  |
|  | 1730 | Shortest Path to Get Food | 54.3% | Medium |  |
|  | 582 | Kill Process | 65.2% | Medium |  |
|  | 617 | Merge Two Binary Trees | 76.8% | Easy |  |
|  | 623 | Add One Row to Tree | 53.5% | Medium |  |
|  | 637 | Average of Levels in Binary Tree | 67.4% | Easy |  |
|  | 652 | Find Duplicate Subtrees | 54.6% | Medium |  |
|  | 653 | Two Sum IV - Input is a BST | 57.9% | Easy |  |
|  | 655 | Print Binary Tree | 57.8% | Medium |  |
|  | 662 | Maximum Width of Binary Tree | 39.6% | Medium |  |
|  | 672 | Bulb Switcher II | 50.8% | Medium |  |
|  | 675 | Cut Off Trees for Golf Event | 35.4% | Hard |  |
|  | 684 | Redundant Connection | 60.4% | Medium |  |
|  | 685 | Redundant Connection II | 33.4% | Hard |  |
|  | 690 | Employee Importance | 61.6% | Easy |  |
|  | 694 | Number of Distinct Islands | 59.0% | Medium |  |
|  | 695 | Max Area of Island | 67.9% | Medium |  |
|  | 711 | Number of Distinct Islands II | 50.6% | Hard |  |
|  | 721 | Accounts Merge | 54.1% | Medium |  |
|  | 733 | Flood Fill | 56.8% | Easy |  |
|  | 737 | Sentence Similarity II | 47.3% | Medium |  |
|  | 742 | Closest Leaf in a Binary Tree | 44.8% | Medium |  |
|  | 743 | Network Delay Time | 47.0% | Medium |  |
|  | 749 | Contain Virus | 49.4% | Hard |  |
|  | 752 | Open the Lock | 55.0% | Medium |  |
|  | 756 | Pyramid Transition Matrix | 55.6% | Medium |  |
|  | 429 | N-ary Tree Level Order Traversal | 68.1% | Medium |  |
|  | 428 | Serialize and Deserialize N-ary Tree | 63.3% | Hard |  |
|  | 765 | Couples Holding Hands | 56.1% | Hard |  |
|  | 431 | Encode N-ary Tree to Binary Tree | 75.7% | Hard |  |
|  | 559 | Maximum Depth of N-ary Tree | 70.3% | Easy |  |
|  | 773 | Sliding Puzzle | 62.4% | Hard |  |
|  | 778 | Swim in Rising Water | 58.0% | Hard |  |
|  | 783 | Minimum Distance Between BST Nodes | 55.2% | Easy |  |
|  | 785 | Is Graph Bipartite? | 49.5% | Medium |  |
|  | 787 | Cheapest Flights Within K Stops | 36.9% | Medium |  |
|  | 797 | All Paths From Source to Target | 79.6% | Medium |  |
|  | 802 | Find Eventual Safe States | 51.2% | Medium |  |
|  | 815 | Bus Routes | 44.5% | Hard |  |
|  | 827 | Making A Large Island | 44.2% | Hard |  |
|  | 839 | Similar String Groups | 43.8% | Hard |  |
|  | 841 | Keys and Rooms | 67.6% | Medium |  |
|  | 847 | Shortest Path Visiting All Nodes | 55.4% | Hard |  |
|  | 854 | K-Similar Strings | 38.7% | Hard |  |
|  | 863 | All Nodes Distance K in Binary Tree | 59.7% | Medium |  |
|  | 864 | Shortest Path to Get All Keys | 43.4% | Hard |  |
|  | 865 | Smallest Subtree with all the Deepest Nodes | 66.5% | Medium |  |
|  | 886 | Possible Bipartition | 46.3% | Medium |  |
|  | 909 | Snakes and Ladders | 39.6% | Medium |  |
|  | 913 | Cat and Mouse | 35.2% | Hard |  |
|  | 919 | Complete Binary Tree Inserter | 62.0% | Medium |  |
|  | 924 | Minimize Malware Spread | 41.8% | Hard |  |
|  | 928 | Minimize Malware Spread II | 41.8% | Hard |  |
|  | 934 | Shortest Bridge | 51.6% | Medium |  |
|  | 958 | Check Completeness of a Binary Tree | 52.9% | Medium |  |
|  | 959 | Regions Cut By Slashes | 68.2% | Medium |  |
|  | 965 | Univalued Binary Tree | 68.4% | Easy |  |
|  | 967 | Numbers With Same Consecutive Differences | 46.4% | Medium |  |
|  | 987 | Vertical Order Traversal of a Binary Tree | 39.7% | Hard |  |
|  | 993 | Cousins in Binary Tree | 53.6% | Easy |  |
|  | 994 | Rotting Oranges | 50.4% | Medium |  |
|  | 1020 | Number of Enclaves | 60.6% | Medium |  |
|  | 1087 | Brace Expansion | 63.9% | Medium |  |
|  | 1102 | Path With Maximum Minimum Value | 51.6% | Medium |  |
|  | 1034 | Coloring A Border | 47.0% | Medium |  |
|  | 1036 | Escape a Large Maze | 34.0% | Hard |  |
|  | 1161 | Maximum Level Sum of a Binary Tree | 67.1% | Medium |  |
|  | 1162 | As Far from Land as Possible | 46.9% | Medium |  |
|  | 1042 | Flower Planting With No Adjacent | 49.3% | Medium |  |
|  | 1197 | Minimum Knight Moves | 39.0% | Medium |  |
|  | 1215 | Stepping Numbers | 44.6% | Medium |  |
|  | 1091 | Shortest Path in Binary Matrix | 41.3% | Medium |  |
|  | 1245 | Tree Diameter | 61.9% | Medium |  |
|  | 1096 | Brace Expansion II | 62.1% | Hard |  |
|  | 1257 | Smallest Common Region | 61.8% | Medium |  |
|  | 1273 | Delete Tree Nodes | 61.2% | Medium |  |
|  | 1123 | Lowest Common Ancestor of Deepest Leaves | 69.0% | Medium |  |
|  | 1129 | Shortest Path with Alternating Colors | 41.3% | Medium |  |
|  | 1315 | Sum of Nodes with Even-Valued Grandparent | 84.8% | Medium |  |
|  | 1302 | Deepest Leaves Sum | 85.6% | Medium |  |
|  | 1236 | Web Crawler | 65.3% | Medium |  |
|  | 1361 | Validate Binary Tree Nodes | 42.1% | Medium |  |
|  | 1483 | Kth Ancestor of a Tree Node | 33.2% | Hard |  |
|  | 1202 | Smallest String With Swaps | 50.9% | Medium |  |
|  | 1203 | Sort Items by Groups Respecting Dependencies | 48.9% | Hard |  |
|  | 1210 | Minimum Moves to Reach Target with Rotations | 47.5% | Hard |  |
|  | 1242 | Web Crawler Multithreaded | 48.2% | Medium |  |
|  | 1254 | Number of Closed Islands | 62.6% | Medium |  |
|  | 1261 | Find Elements in a Contaminated Binary Tree | 75.3% | Medium |  |
|  | 1263 | Minimum Moves to Move a Box to Their Target Location | 47.5% | Hard |  |
|  | 1267 | Count Servers that Communicate | 57.9% | Medium |  |
|  | 1284 | Minimum Number of Flips to Convert Binary Matrix to Zero Matrix | 70.7% | Hard |  |
|  | 1293 | Shortest Path in a Grid with Obstacles Elimination | 44.0% | Hard |  |
|  | 1298 | Maximum Candies You Can Get from Boxes | 60.6% | Hard |  |
|  | 1306 | Jump Game III | 61.6% | Medium |  |
|  | 1430 | Check If a String Is a Valid Sequence from Root to Leaves Path in a Binary Tree | 45.4% | Medium |  |
|  | 1311 | Get Watched Videos by Your Friends | 44.6% | Medium |  |
|  | 1319 | Number of Operations to Make Network Connected | 56.2% | Medium |  |
|  | 1345 | Jump Game IV | 42.1% | Hard |  |
|  | 1325 | Delete Leaves With a Given Value | 74.6% | Medium |  |
|  | 1367 | Linked List in Binary Tree | 42.2% | Medium |  |
|  | 1368 | Minimum Cost to Make at Least One Valid Path in a Grid | 59.4% | Hard |  |
|  | 1376 | Time Needed to Inform All Employees | 57.9% | Medium |  |
|  | 1377 | Frog Position After T Seconds | 36.0% | Hard |  |
|  | 1379 | Find a Corresponding Node of a Binary Tree in a Clone of That Tree | 85.1% | Medium |  |
|  | 1391 | Check if There is a Valid Path in a Grid | 46.2% | Medium |  |
|  | 1448 | Count Good Nodes in Binary Tree | 73.0% | Medium |  |
|  | 1443 | Minimum Time to Collect All Apples in a Tree | 55.2% | Medium |  |
|  | 1462 | Course Schedule IV | 46.9% | Medium |  |
|  | 1457 | Pseudo-Palindromic Paths in a Binary Tree | 68.0% | Medium |  |
|  | 1466 | Reorder Routes to Make All Paths Lead to the City Zero | 61.6% | Medium |  |
|  | 1469 | Find All The Lonely Nodes | 81.1% | Easy |  |
|  | 1485 | Clone Binary Tree With Random Pointer | 79.2% | Medium |  |
|  | 1490 | Clone N-ary Tree | 82.8% | Medium |  |
|  | 1519 | Number of Nodes in the Sub-Tree With the Same Label | 38.6% | Medium |  |
|  | 1559 | Detect Cycles in 2D Grid | 46.7% | Medium |  |
|  | 1568 | Minimum Number of Days to Disconnect Island | 49.6% | Hard |  |
|  | 1728 | Cat and Mouse II | 41.4% | Hard |  |
|  | 1609 | Even Odd Tree | 52.6% | Medium |  |
|  | 1602 | Find Nearest Right Node in Binary Tree | 73.7% | Medium |  |
|  | 1625 | Lexicographically Smallest String After Applying Operations | 66.0% | Medium |  |
|  | 1631 | Path With Minimum Effort | 50.9% | Medium |  |
|  | 1654 | Minimum Jumps to Reach Home | 25.3% | Medium |  |
|  | 1660 | Correct a Binary Tree | 73.6% | Medium |  |
|  | 1766 | Tree of Coprimes | 37.6% | Hard |  |
|  | 1765 | Map of Highest Peak | 58.0% | Medium |  |
|  | 1740 | Find Distance in a Binary Tree | 68.5% | Medium |  |
|  | 1778 | Shortest Path in a Hidden Grid | 44.3% | Medium |  |
|  | 1810 | Minimum Path Cost in a Hidden Grid | 53.2% | Medium |  |
|  | 1905 | Count Sub Islands | 61.6% | Medium |  |
|  | 1926 | Nearest Exit from Entrance in Maze | 36.5% | Medium |  |
|  | 1970 | Last Day Where You Can Still Cross | 47.8% | Hard |  |
|  | 1992 | Find All Groups of Farmland | 64.4% | Medium |  |
|  | 1993 | Operations on Tree | 39.5% | Medium |  |
|  | 1971 | Find if Path Exists in Graph | 50.2% | Easy |  |
|  | 2039 | The Time When the Network Becomes Idle | 45.8% | Medium |  |
|  | 2045 | Second Minimum Time to Reach Destination | 32.0% | Hard |  |
