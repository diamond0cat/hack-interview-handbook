- 这个题目有基本版和follow-up版
- 需要clarify的点：
  - 1.sorted or unsorted
  - 2. about duplicates
      - {1,1,3,3} target = 4
        - return 1 - if we don't count duplicate pairs
        - return 4, if we count duplicate pairs

- 需要clarify的点：given a sorted array, hwo many pair sum == target
    - the input array possibly with duplicate
    - how we count duplicate pairs



- v0: no duplicate elemtns in the input array, 这种情况不用考虑去重

  ```java




  ```


- v1: 有重复，不算重复



- v2: 有重复，算重复，每个index作为一个单独的元素处理
    - count 重复的i的个数和j的个数，两个count乘法求积
    - i count的时候每次停在group的最左侧, j每次停在group最后侧
    - 还有一个Corner case没处理：  i 和j的元素相等的时候

