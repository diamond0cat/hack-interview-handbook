

```java
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        // nums[i] + nums[j] + nums[k] = 0
        // nums[j] + nums[k] = -nums[i]
        // i < j < k
        vector<vector<int>> ans;
        for (int i = 0; i < nums.size(); i++) {
            if (i > 0 && nums[i] == nums[i - 1]) continue;//去重，数组下标预判
            auto all_two_sums = twoSum(nums, i + 1, -nums[i]);
            for (auto jk : all_two_sums) {
                ans.push_back({nums[i], jk[0], jk[1]});
            }
        }
        return ans;
    }
private:
    vector<vector<int>> twoSum(vector<int>& numbers, int start, int target) {
        vector<vector<int>> ans;
        int j = numbers.size() - 1;//j从右到左
        for (int i = start; i < numbers.size(); i++) {
            if (i > start && numbers[i] == numbers[i - 1]) continue;//去重
            while (i < j && numbers[i] + numbers[j] > target) j--; //如果太大了，j--
            if (i < j && numbers[i] + numbers[j] == target) {
                ans.push_back({numbers[i], numbers[j]});
            }
        }
        return ans;
    }
};

```