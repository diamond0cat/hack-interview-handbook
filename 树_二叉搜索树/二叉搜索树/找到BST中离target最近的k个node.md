
- sliding window of size k in BST

- in roder traversal, BsT => sorted array
- queue = [all number sin the sliding window of size k]

- queue = [the first k numbers]
  - for each step
    - if the number to eat is closer to target than the number to throw away
      - move sliding window to the right by one step
    - else
      - return queue



space = O(1) time = O(n)


