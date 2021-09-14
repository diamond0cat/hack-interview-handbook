SC = O(n^2)
TC = O(n!)


怎么去重? dedup是针对当前这个node往下所有的分支来做的，每一个node对应一个recursion call



![picture 12](https://i.loli.net/2021/09/15/rIme5j9wFW2QhME.png)  


```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        if (nums == null) {
            return result;
        }
       
        helper(result,  nums, 0);
        return result;
    }
    

     private void helper(List<List<Integer>> result, int[] nums, int index) {
        if (index == nums.length) {
            List<Integer> cur = new ArrayList<>();
            for (int i = 0; i < nums.length ;i++) {
                cur.add(nums[i]);
            }
            result.add(cur);
            return;
        }
        HashSet<Integer> used = new HashSet<>();
        for (int i = index; i < nums.length; i++){  // 容易错的地方
           if (!used.contains(nums[i])) {  //在每一个节点explore出去的时候剪枝
               used.add(nums[i]);
               swap(nums, index, i);
               helper(result, nums, index + 1);
               swap(nums, index, i);
           } 
            
        }
    }

    private void swap(int[] nums, int i, int j) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}
```

![picture 1](https://i.loli.net/2021/09/10/TmlB8K2OGCSn6fZ.png)  
