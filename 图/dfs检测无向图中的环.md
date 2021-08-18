有向图的环检测和无向图一样的

深度优先遍历该图，如果在遍历的过程中，发现某个节点有一条边指向已经访问过的节点，并且这个已访问过的节点不是当前节点的上一个节点（这里的父节点表示dfs遍历顺序中的上一个节点），则表示存在环。但是我们不能仅仅使用一个bool数组来标志节点是否访问过。

对每个节点分为三种状态，白、灰、黑。
开始时所有节点都是白色，当开始访问某个节点时该节点变为灰色，当该节点的所有邻接点都访问完，该节点颜色变为黑色。

那么我们的算法则为：如果遍历的过程中发现某个节点有一条边指向颜色为灰的节点，那么存在环。


```java
public class CycleDetection {

    private Graph G;
    private boolean[] visited;
    private boolean hasCycle = false;

    public CycleDetection(Graph G){

        this.G = G;
        visited = new boolean[G.V()];
        for(int v = 0; v < G.V(); v ++)
            if(!visited[v])
                if(dfs(v, v)){
                    hasCycle = true;
                    break;
                }
    }

    // 从顶点 v 开始，判断图中是否有环
    private boolean dfs(int v, int parent){

        visited[v] = true;
        for(int w: G.adj(v))
            if(!visited[w]){
                if(dfs(w, v)) return true;
            } else if(w != parent)
                return true;
        return false;
    }

    public boolean hasCycle(){
        return hasCycle;
    }

    public static void main(String[] args){

        Graph g = new Graph("g.txt");
        CycleDetection cycleDetection = new CycleDetection(g);
        System.out.println(cycleDetection.hasCycle());

        Graph g2 = new Graph("g2.txt");
        CycleDetection cycleDetection2 = new CycleDetection(g2);
        System.out.println(cycleDetection2.hasCycle());
    }
}
```