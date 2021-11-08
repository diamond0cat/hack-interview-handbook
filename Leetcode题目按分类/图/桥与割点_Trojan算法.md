![20210821172207](https://i.loli.net/2021/08/22/WcZIu3s1jGAft6O.png)


寻找桥的算法： dfs, 遍历的过程记录不同的信息，根据记录的信息组合出逻辑，从而求出答案
寻找桥的算法更难，因为记录的信息更多元

怎么更新信息，怎么维护信息，怎么使用信息

order数组记录遍历的顺序
low数组记录对每个顶点来说，通过它从另外一条路能到达的最低的那个order值



 ![20210822225115](https://i.loli.net/2021/08/23/V2XlbMGvEs9cj1I.png)


![20210821233823](https://i.loli.net/2021/08/22/pLrK982Sncs4EIu.png)
![20210821235122](https://i.loli.net/2021/08/22/GUHXbrxvkO1zYRt.png)



![20210821235302](https://i.loli.net/2021/08/22/4u9ACHrJBj7Ikdv.png)

![20210821235820](https://i.loli.net/2021/08/22/5ozygJVaCRPWFTk.png)


树是将图中所有顶点连接起来所用边数最少的情况，

![20210822111337](https://i.loli.net/2021/08/23/6kyIoFMcHX4DTzP.png)


图的遍历树: bfs遍历树，dfs遍历树

dfs遍历树：前向边和后向边，前向边：遍历树上的边，后向边：不在遍历树上的边

图中的后向边可以只想自己的祖先节点，我们就是利用这个特性找到图中的桥
![20210822103210](https://i.loli.net/2021/08/23/2dw6zTQ7FvNUI3J.png)

寻找割点:

![20210822222208](https://i.loli.net/2021/08/23/xBGgOks86vamDCH.png)

![20210822222438](https://i.loli.net/2021/08/23/9vbOVqNEhPY1TQl.png)



### 寻找桥的算法：  dfs
```java


import java.util.ArrayList;

public class FindBridges {

    private Graph G;
    private boolean[] visited;

    private int ord[];
    private int low[];
    private int cnt;

    private ArrayList<Edge> res;

    public FindBridges(Graph G){

        this.G = G;
        visited = new boolean[G.V()];

        res = new ArrayList<>();
        ord = new int[G.V()];
        low = new int[G.V()];
        cnt = 0;

        for(int v = 0; v < G.V(); v ++)
            if(!visited[v])
                dfs(v, v);
    }

    private void dfs(int v, int parent){

        visited[v] = true;
        ord[v] = cnt;
        low[v] = ord[v];
        cnt ++;

        for(int w: G.adj(v))
            if(!visited[w]){
                dfs(w, v);
                low[v] = Math.min(low[v], low[w]);
                if(low[w] > ord[v])
                    res.add(new Edge(v, w));
            }
            else if(w != parent)
                low[v] = Math.min(low[v], low[w]);
    }

    public ArrayList<Edge> result(){
        return res;
    }

    public static void main(String[] args){

        Graph g = new Graph("g.txt");
        FindBridges fb = new FindBridges(g);
        System.out.println("Bridges in g : " + fb.result());

        Graph g2 = new Graph("g2.txt");
        FindBridges fb2 = new FindBridges(g2);
        System.out.println("Bridges in g2 : " + fb2.result());

        Graph tree = new Graph("tree.txt");
        FindBridges fb3 = new FindBridges(tree);
        System.out.println("Bridges in tree : " + fb3.result());
    }
}

```


```java
import java.util.HashSet;

public class FindCutPoints {

    private Graph G;
    private boolean[] visited;

    private int[] ord;
    private int[] low;
    private int cnt;

    private HashSet<Integer> res;

    public FindCutPoints(Graph G){

        this.G = G;
        visited = new boolean[G.V()];

        res = new HashSet<>();
        ord = new int[G.V()];
        low = new int[G.V()];
        cnt = 0;

        for(int v = 0; v < G.V(); v ++)
            if(!visited[v])
                dfs(v, v);
    }

    private void dfs(int v, int parent){

        visited[v] = true;
        ord[v] = cnt;
        low[v] = ord[v];
        cnt ++;

        int child = 0;

        for(int w: G.adj(v))
            if(!visited[w]){
                dfs(w, v);
                low[v] = Math.min(low[v], low[w]);

                if(v != parent && low[w] >= ord[v])
                    res.add(v);

                child ++;
                if(v == parent && child > 1)
                    res.add(v);
            }
            else if(w != parent)
                low[v] = Math.min(low[v], low[w]);
    }

    public HashSet<Integer> result(){
        return res;
    }

    public static void main(String[] args){

        Graph g = new Graph("g.txt");
        FindCutPoints fc = new FindCutPoints(g);
        System.out.println("Cut Points in g : " + fc.result());

        Graph g2 = new Graph("g2.txt");
        FindCutPoints fc2 = new FindCutPoints(g2);
        System.out.println("Cut Points in g2 : " + fc2.result());

        Graph tree = new Graph("tree.txt");
        FindCutPoints fc3 = new FindCutPoints(tree);
        System.out.println("Cut Points in tree : " + fc3.result());
    }
}

```