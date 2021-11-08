
红黑树比哈希表更节省空间


```java
import java.io.File;
import java.io.IOException;
import java.util.TreeSet;
import java.util.Scanner;

public class AdjSet {

    private int V;
    private int E;
    private TreeSet<Integer>[] adj;

    public AdjSet(String pathStr){

        File file = new File(pathStr);

        try(Scanner scanner = new Scanner(file)){

            V = scanner.nextInt();
            if(V < 0) throw new IllegalArgumentException("V must be non-negative");
            adj = new TreeSet[V];
            for(int i = 0; i < V; i ++)
                adj[i] = new TreeSet<Integer>();

            E = scanner.nextInt();
            if(E < 0) throw new IllegalArgumentException("E must be non-negative");

            for(int i = 0; i < E; i ++){
                int a = scanner.nextInt();
                validateVertex(a);
                int b = scanner.nextInt();
                validateVertex(b);

                if(a == b) throw new IllegalArgumentException("Self Loop is Detected!");
                if(adj[a].contains(b)) throw new IllegalArgumentException("Parallel Edges are Detected!");

                adj[a].add(b);
                adj[b].add(a);
            }
        }
        catch(IOException e){
            e.printStackTrace();
        }
    }

    private void validateVertex(int v){
        if(v < 0 || v >= V)
            throw new IllegalArgumentException("vertex " + v + "is invalid");
    }

    public int V(){
        return V;
    }

    public int E(){
        return E;
    }

    public boolean hasEdge(int v, int w){
        validateVertex(v);
        validateVertex(w);
        return adj[v].contains(w);
    }

    public Iterable<Integer> adj(int v){   //返回iterable
    // public TreeSet<Integer> adj(int v){
        validateVertex(v);
        return adj[v];
    }

    public int degree(int v){
        validateVertex(v);
        return adj[v].size();
    }

    @Override
    public String toString(){
        StringBuilder sb = new StringBuilder();

        sb.append(String.format("V = %d, E = %d\n", V, E));
        for(int v = 0; v < V; v ++){
            sb.append(String.format("%d : ", v));
            for(int w : adj[v])
                sb.append(String.format("%d ", w));
            sb.append('\n');
        }
        return sb.toString();
    }

    public static void main(String[] args){

        AdjSet adjSet = new AdjSet("g.txt");
        System.out.print(adjSet);
    }
}

```


```java
package com.laioffer;


import java.io.File;
import java.io.IOException;
import java.util.ArrayList;
import java.util.TreeSet;
import java.util.Scanner;

public class AdjSet {

    private int V;
    private int E;
    private  TreeSet<Integer>[] adj;  //图里有多少个顶点就创建多少个链表

    public AdjSet(String filename){

        File file = new File(filename);

        try(Scanner scanner = new Scanner(file)){

            V = scanner.nextInt();
            if(V < 0) throw new IllegalArgumentException("V must be non-negative");
            adj = new TreeSet[V];
            for (int i = 0; i < V; i++) {
                adj[i] = new TreeSet<Integer>();
            }
            E = scanner.nextInt();
            if(E < 0) throw new IllegalArgumentException("E must be non-negative");

            for(int i = 0; i < E; i ++){
                int a = scanner.nextInt();
                validateVertex(a);
                int b = scanner.nextInt();
                validateVertex(b);

                if(a == b) throw new IllegalArgumentException("Self Loop is Detected!");
                // time = O(V) 节点的边最多有V-1条
                if(adj[a].contains(b)) throw new IllegalArgumentException("Parallel Edges are Detected!");

                adj[a].add(b);
                adj[b].add(a);
            }
        }
        catch(IOException e){
            e.printStackTrace();
        }
    }

    public void validateVertex(int v){
        if(v < 0 || v >= V)
            throw new IllegalArgumentException("vertex " + v + "is invalid");
    }

    public int V(){
        return V;
    }

    public int E(){
        return E;
    }

    public boolean hasEdge(int v, int w){
        validateVertex(v);
        validateVertex(w);
        return adj[v].contains(w);
    }

    public Iterable<Integer> adj(int v){
        validateVertex(v);
        return adj[v];
    }

    public int degree(int v){
        validateVertex(v);
        return adj[v].size();
    }

    //返回每个联通分量和所有的node,n个联通分量就有n个arraylist
    public List<Integer>[] components() {
        List<Integer>[] res = new ArrayList<>[cccount];
        //对每个linkedlist开空间
        for (int i = 0; i < cccount; i++) {
            res[i] = new ArrayList<Integer>();
        }
        //遍历图中所有顶点
        for (int v = 0; v < G.V(); v++) {
            res[visited[V]].add(v);
        }
        return res;
    }

    //  判断是否属于同一个联通分量
    public boolean isConnected(int v, int w) {
        validateVertex(v);
        validateVertex(w);
        return visited[v] == visited[w];
    }
    //返回联通分量的总数
    public int count() {
        for (int e : visited) {
            System.out.println(e + " ");
        }
        System.out.println();
        return ccount;
    }

    @Override
    public String toString(){
        StringBuilder sb = new StringBuilder();

        sb.append(String.format("V = %d, E = %d\n", V, E));
        for(int v = 0; v < V; v ++){
            sb.append(String.format("%d :", v));
            for(int w : adj[v])  // adj[v].get(0) = 3  这里0只是一个索引
                sb.append(String.format("%d ", w));
            sb.append('\n');
        }
        return sb.toString();
    }

    public static void main(String[] args){

        AdjSet adjSet = new AdjSet("g.txt");
        System.out.print(adjSet);
    }
}


```