- 2-diff, how many pairs diff = target (< target, > target), where target > 0


  - v1. array is sorted - assume no duplicate
    - (1,2,3,4) target = 2, return 2
    - solution: sliding window
      - 分解所有的pair: i < j
        - 固定j:
          - for all j:
              - check if there is any i < j, such that array[i] + target == array[j]
      - 为什么这个方法不会漏解：  j -> move right,  is is guarantee not moving left(stay or move right)   