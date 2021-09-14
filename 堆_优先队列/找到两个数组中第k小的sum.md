![picture 10](https://i.loli.net/2021/09/14/ra9Ao4fBqGLU6Ht.png)  


- time = 2 k * logk
- space = m*n + k  //每次拿一个出来塞两个进去，最多干k轮, m*n是visited matrix占用的空间
  
```java
public class Solution {
  public int kthSum(int[] A, int[] B, int k) {
    // best first search, assum input are valid
    boolean[][] visited = new boolean[A.length][B.length];
    PriorityQueue<Cell> pq = new PriorityQueue<>(new Comparator<Cell>(){
      // sort cell by it's value ascending
      @Override
      public int compare(Cell c1, Cell c2) {
        return c1.val - c2.val;
      }
    });

    pq.offer(new Cell(0, 0, A[0] + B[0]));
    visited[0][0] = true;   // deduplication

    for (int i = 0; i < k - 1 ; i++) {
      Cell c = pq.poll();
      int x = c.i;
      int y = c.j;
      if (x + 1 < A.length && !visited[x + 1][y]) {
        visited[x +1][y] = true;
        pq.offer(new Cell(x +1, y, A[x+1] +B[y]));
      }
      if (y + 1 < B.length && !visited[x][y + 1]) {
        visited[x][y + 1] = true;
        pq.offer(new Cell(x, y + 1, A[x] +B[y + 1]));
      }
    }
    return pq.peek().val;

  }
  static class Cell {
    int i;
    int j;
    int val;
    Cell(int i, int j, int val) {
      this.i = i;
      this.j = j;
      this.val = val;
    }
  }
}

```