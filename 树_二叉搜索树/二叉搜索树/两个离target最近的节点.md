
- 暴力： inorder traverse and get a sorted list  --> find closest node to target, and closest - 1, cloest + 1中拿更近的那个


- solution 2: find closest不需要先转换为sorted array在做binary search, binary search的过程就对应到了在bst中search一个elemenet的过程
        - search closest
        - search largestSmaller
        - search smalelstLarger
        - time = O(3*logn)


