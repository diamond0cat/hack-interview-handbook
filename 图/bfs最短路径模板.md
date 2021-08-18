
![20210818113140](https://i.loli.net/2021/08/19/uAJ51kMtlFPzw7U.png)

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.LinkedList;
import java.util.Queue;

// Unweighted Single Source Shortest Path
public class USSSPath {

    private Graph G;
    private int s;

    private boolean[] visited;
    private int[] pre;
    private int[] dis;   // 存储distance from start to i,有多少个顶点开多少空间

    public USSSPath(Graph G, int s){

        this.G = G;
        this.s = s;

        visited = new boolean[G.V()];
        pre = new int[G.V()];
        dis = new int[G.V()];
        for(int i = 0; i < G.V(); i ++) {
            pre[i] = -1;
            dis[i] = -1;   //初始化为-1，-1表示不能到达
        }
        bfs(s);

        for(int i = 0; i < G.V(); i ++)
            System.out.print(dis[i] + " ");
        System.out.println();
    }

    private void bfs(int s){

        Queue<Integer> queue = new LinkedList<>();
        queue.add(s);
        visited[s] = true;
        pre[s] = s;
        dis[s] = 0;   //源点s到源点s的距离为零
        while(!queue.isEmpty()){
            int v = queue.remove();

            for(int w: G.adj(v))
                if(!visited[w]){
                    queue.add(w);
                    visited[w] = true;
                    pre[w] = v;
                    dis[w] = dis[v] + 1;  //距离+1
                }
        }
    }

    public boolean isConnectedTo(int t){
        G.validateVertex(t);
        return visited[t];
    }

    public int dis(int t){
        G.validateVertex(t);
        return dis[t];
    }

    public Iterable<Integer> path(int t){

        ArrayList<Integer> res = new ArrayList<Integer>();
        if(!isConnectedTo(t)) return res;

        int cur = t;
        while(cur != s){
            res.add(cur);
            cur = pre[cur];
        }
        res.add(s);

        Collections.reverse(res);
        return res;
    }

    public static void main(String[] args){

        Graph g = new Graph("g.txt");
        USSSPath ussspath = new USSSPath(g, 0);
        System.out.println("0 -> 6 : " + ussspath.path(6));
        System.out.println("0 -> 6 : " + ussspath.dis(6));
    }
}

```