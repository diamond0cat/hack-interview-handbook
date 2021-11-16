

- solution 1: prefix sum 
    - time=O(n^2)

- solution  2: hashMap + prefixSum 
    -  time=O(n)
 ```java
     public int subarraySumEqualsKII(int[] nums, int k) {
        // sanity check
        // sum :index
        Map<Integer, Integer> map = new HashMap<>();

        int curSum = 0;
        map.put(0, -1);   //前0个数的前缀和为0
        int minLen = Integer.MAX_VALUE;

        for (int i = 0; i < nums.length; i++) {
            curSum += nums[i];

            if (map.containsKey(curSum - k)) {
                minLen = Math.min(minLen, i - map.get(curSum - k));
            }
            map.put(curSum, i);
        }
        return minLen;
    }
    ```


```java
    public int subarraySumEqualsKII(int[] nums, int k) {

       // 前缀和 -> 前缀和数组的index
       Map<Long, Integer> sumToIndex = new HashMap<>();
       // 这一个行的目的： 
       sumToIndex.put((long)0, 0);  // prefixSum: index  前缀和数组下标从0开始

       long prefixSum = 0;
       int minLen = Integer.MAX_VALUE;
      
       for (int i = 0; i < nums.length; i++) {
           prefixSum += (long)nums[i];
 
           if (sumToIndex.containsKey(prefixSum - k)) {
               int len = i + 1 - sumToIndex.get(prefixSum - k);
               minLen = Math.min(minLen, len);
           }
           sumToIndex.put(prefixSum, i + 1);
       }
      return minLen == Integer.MAX_VALUE ? -1 :minLen;
    }

```


- 如果这题求最长的：

 
```java
    public int subarraySumEqualsKII(int[] nums, int k) {

       // 前缀和 -> 前缀和数组的index
       Map<Long, Integer> sumToIndex = new HashMap<>();
       // 这一个行的目的： 
       sumToIndex.put((long)0, 0);  // prefixSum: index  前缀和数组下标从0开始

       long prefixSum = 0;
       int maxLen = Integer.MIN_VALUE;
      
       for (int i = 0; i < nums.length; i++) {
           prefixSum += (long)nums[i];
 
           if (sumToIndex.containsKey(prefixSum - k)) {
               int len = i + 1 - sumToIndex.get(prefixSum - k);
               maxLen = Math.max(maxLen, len);
           }
           sumToIndex.putIfAbsent(prefixSum, i + 1);  //只记最小的下标
       }
      return minLen == Integer.MAX_VALUE ? -1 :minLen;
    }

```