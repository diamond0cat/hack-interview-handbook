- 给定字符串str，和一个字典dict, 需要找出字典里那些单词是str的子序列， 返回这些单词
  - str="bcogtadsjofisdhklasdj"
  - dict=["book", "code", "tag"]
  - 输出: ["book']


- native solution ：谁小移谁  time=O(m*n)  m为单词个数，n个单词长度



- solution 2:预处理 + 前缀和数组 + 从后往前扫描递推  ==》 这个思想跟coun smaller after itself那道题的思想很像


- 

- 


```java
public class Solution {
    /**
     * @param str: the string
     * @param dict: the dictionary
     * @return: return words which  are subsequences of the string
     */
    public List<String> findWords(String str, List<String> dict) {
        List<String> ans = new ArrayList<>();
        if (str == null || str.length() == 0)
            return ans;
        int n = str.length();
        int[][] positions = new int[n + 1][26];
        initialization(positions, str);
        for (String cur : dict) {
            if (findWord(cur, positions))
                ans.add(cur);
        }
        return ans;
    }
    private void initialization(int[][] positions, String str) {
        int n = str.length();
        for (int i = 0; i < 26; i++) {
            positions[n][i] = n + 1;
        }
        for (int i = n - 1; i >= 0; i--) {
            for (int j = 0; j < 26; j++) {
                positions[i][j] = positions[i + 1][j];
            }
            positions[i][str.charAt(i) - 'a'] = i + 1;
        }
    }
    private boolean findWord(String str, int[][] positions) {
        int n = positions.length - 1;
        int j = 0;
        for (int i = 0; i < str.length(); i++) {
            char ch = str.charAt(i);
            j = positions[j][ch - 'a'];
            if (j == n + 1)
                break;
        }
        return j != n + 1;
    }
}
```