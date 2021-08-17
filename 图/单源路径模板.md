
可以求出从一个起点开始到任意节点的路径，
如果要求从某一个点开始到其他点的路径，就要从这个起点开始做DFS

dfs同时记录pre信息


找到目标点后，提前终止DFSs
![20210817141430](https://i.loli.net/2021/08/18/sD3JKg5AQaIxiXE.png)


![20210817125254](https://i.loli.net/2021/08/18/XVCkv8O7qlyYRDt.png)


```java
import java.util.ArrayList;
import java.util.Collections;

public class SingleSourcePath {

    private Graph G;
    private int s;

    private boolean[] visited;
    private int[] pre;  //

    public SingleSourcePath(Graph G, int s){ //S是开始的节点，源节点

        G.validateVertex(s);  //validate user input

        this.G = G;
        this.s = s;
        visited = new boolean[G.V()];
        pre = new int[G.V()];      //有多少个顶点，就开多少个空间

        //这里我们只需要针对s为起点求路径，所以只从s开始就可以了
        dfs(s, s);  //这里只能遍历到s所能到达的vertexS ，第2个参数表示parent,根节点的父亲节点是他自己
    }

    private void dfs(int v, int parent){

        visited[v] = true;
        pre[v] = parent;   //把当前节点的前一个节点放入pre数组
        for(int w: G.adj(v))
            if(!visited[w])
                dfs(w, v);
    }

    public boolean isConnectedTo(int t){
        G.validateVertex(t);
        return visited[t];  //如果t被遍历到了，t一定跟s连通
    }

    public Iterable<Integer> path(int t){

        ArrayList<Integer> res = new ArrayList<Integer>();
        if(!isConnectedTo(t)) return res;  //不连通的情况返回空链表

        int cur = t;
        while(cur != s){  //找到source node了循环就结束了
            res.add(cur);
            cur = pre[cur];   //顺着target节点在pre数组里从后往前找
        }
        res.add(s);

        Collections.reverse(res);  //路径必须从起点开始在终点结束
        return res;
    }

    public static void main(String[] args){

        Graph g = new Graph("g.txt");
        SingleSourcePath sspath = new SingleSourcePath(g, 0);
        System.out.println("0 -> 6 : " + sspath.path(6));
        System.out.println("0 -> 5 : " + sspath.path(5));
    }
}

```


### 另一种写法，省去了visited数组，只使用pre数组，既表示visited信息，又表示前驱节点，visited[i]=-1的时候表示没有前驱，否则存储前驱节点

```java
import java.util.ArrayList;
import java.util.Collections;

public class SingleSourcePath {

    private Graph G;
    private int s;

    private int[] pre;

    public SingleSourcePath(Graph G, int s){

        this.G = G;
        this.s = s;
        pre = new int[G.V()];
        for(int i = 0; i < pre.length; i ++)
            pre[i] = -1;

        dfs(s, s);
    }

    private void dfs(int v, int parent){

        pre[v] = parent;
        for(int w: G.adj(v))
            if(pre[w] == -1)
                dfs(w, v);
    }

    public boolean isConnectedTo(int t){
        G.validateVertex(t);
        return pre[t] != -1;
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
        SingleSourcePath sspath = new SingleSourcePath(g, 0);
        System.out.println("0 -> 6 : " + sspath.path(6));
        System.out.println("0 -> 5 : " + sspath.path(5));
    }
}

```