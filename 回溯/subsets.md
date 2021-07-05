

```java

class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        
        List<Integer> cur = new ArrayList<>();
        
        dfs(res, cur, nums, 0);
        
        return res;
    }
    
    private void dfs(List<List<Integer>> res, List<Integer> cur, int[] nums, int index) {
        // base case
        if (index >= nums.length) {
            res.add(new ArrayList<>(cur));
            return;
        }
        // add
        cur.add(nums[index]);
        dfs(res, cur, nums, index + 1);
        cur.remove(cur.size() - 1);
        // not add
        
        dfs(res, cur, nums, index + 1);
    }
}

```