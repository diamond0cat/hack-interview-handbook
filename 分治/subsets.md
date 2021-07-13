


solution 1: backtracking,取或不取
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

solution 2: pure recursion

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if (nums == null) return res;
        return allSubsets(nums, 0);
    }

    private List<List<Integer>> allSubsets(int[] array, int index) {
        if (index == array.length) {
            List<Integer> subset = new ArrayList<>();
            List<List<Integer>> result = new ArrayList<>();
            result.add(subset);
            return result;
        }
        // sub-problems
        List<List<Integer>> subSolutions = allSubsets(array, index +  1);
        List<List<Integer>> result = new ArrayList<>();
        // case 1:add
        for (List<Integer> list : subSolutions) {
            List<Integer> tmp = new ArrayList<>(list);
            tmp.add(array[index]);
            result.add(tmp);
        }
        // case 2:not add
        result.addAll(subSolutions);
        return result;
    }
}

```


solution 2: DP  从右到左,由dependency graph的熟悉
时间复杂度并没有改变，comparing to backtracking


defintion :dp[i] = all subsets using subarray[i, array.length - 1]

induction rule: ....
    dp[i] = dp[i + 1] + {for all subsets in dp[i + 1] , concatenant array[i]}    //最小号问题在最右侧，最大号问题在最左侧,从右往左

base case  = dp[array.length] = {{}}
result: dp[0]

```java
    public List<List<Integer>> subsets(int[] nums) {
        // base case: dp[array.length]
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> subset = new ArrayList<>();  // empty set
        result.add(subset);
        
        for (int i = nums.length - 1; i >= 0; i--) {
            int size = result.size();  //dp[i + 1]所有的subset
            for (int j = 0;j <size; j++) {
                subset = new ArrayList<>(result.get(j));
                subset.add(nums[i]);
                result.add(subset);                                     
            }
            
        }
        //dp[0]
        return result;  
    }     
}
```

solution 3: 

//从左往右
definition:‌ ‌dp[i]‌ ‌=‌ ‌all‌ ‌subsets‌ ‌using‌ ‌‌subarray[0,‌ ‌i]‌ ‌
induction‌ ‌rule:‌ ‌
    dp[i]‌ ‌=‌ ‌{dp[i-1]}‌ ‌+‌ ‌{for‌ ‌all‌ ‌subset‌ ‌in‌ ‌dp[i-1],‌ ‌concatenate‌ ‌array[i]}‌

base‌ ‌case‌ ‌=‌ ‌dp[-1]‌ ‌=‌ ‌{{}}‌ ‌

result:‌ ‌dp[array.length‌ ‌-‌ ‌1]‌ ‌

```java

class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        // base case: dp[-1]
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> subset = new ArrayList<>();  // empty set
        result.add(subset);
        
        for (int i = 0; i < nums.length; i++) {
            int size = result.size();  //dp[i-1]所有的subset
            for (int j = 0;j <size; j++) {
                subset = new ArrayList<>(result.get(j));
                subset.add(nums[i]);
                result.add(subset);                                     
            }
            
        }
        //dp[array.legnth - 1]
        return result;  
    }     
}
```