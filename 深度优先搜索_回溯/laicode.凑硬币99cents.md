print all combinations of coins that can sum up to a total value n.

e.g. total value n  = 99 cents
coin value = 25 10 5 1 cent

one possible way:
3*25
2*10
0*5
4*1

```java
public class Solution {
  public List<List<Integer>> combinations(int target, int[] coins) {
    // Write your solution here
    List<List<Integer>> res = new ArrayList<List<Integer>>();
    List<Integer> sol = new ArrayList<>();
    if (target == 0) {
      return res;
    }

    helper(res, sol, target, coins, 0);
    return res;
  }

  private void helper(List<List<Integer>> res, List<Integer> sol, int moneyLeft, int[] coins, int index) {
    // 到了最后一层，能整除的话才会算到结果里， 否则直接返回
    if (index == coins.length - 1) {
      if (moneyLeft % coins[index] == 0) {
          sol.add(moneyLeft / coins[index]);
          res.add(new ArrayList<Integer>(sol));
          sol.remove(sol.size() - 1);
      }
      return;
    }
    for (int i = 0; i <= moneyLeft / coins[index]; i++) {  //i表示当前币种的个数
      sol.add(i);  //这个是append,所以要remove，如果是overwrite,不需要remove
      helper(res, sol, moneyLeft - i * coins[index], coins, index + 1);
      sol.remove(sol.size() - 1);
    }
  }
}

```


![picture 1](https://i.loli.net/2021/09/07/89OeL7MzWHPNG1q.png)  
