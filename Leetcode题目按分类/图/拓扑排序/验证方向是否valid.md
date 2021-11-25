

- 给一串direction， 比如"ANC"意味着A在C的北边，写一个function验证这些function是否valid
  - Note:  A N C,  A NE C 同时出现是否合法
  - 例子: 下面这个不合法,因为A N C, C NE D 所以不可能 A S D

 - solution 1: topological sort

```java
package Graph;
import java.util.*;

public class DirValidator {
    public boolean validate(String[] strings) {
        // process directions strings and build graph
        /*
           需要两个图：一个表示南北向，另一个表示东西向
            做两个转化：
               1. A S D  ==>  D N A    //南北向的图是表示谁在谁的北边

               2. A NE C ==>  A N C   +  A E C  //东西向的图只表示谁在谁的东边
                   NE, SW这种情况需要在两个图里都建立边
           然后分别在这两个图里找环(run topological sort)
         */
        Map<String, Set<String>> NS = new HashMap<>();
        Map<String, Set<String>> EW = new HashMap<>();
        // construct graph
        for (String str :strings) {
            String[] splited = str.split("\\s+");
            // A  N  C
            // N S
            String s1 = splited[0], dirs = splited[1], s2 = splited[2];
            for (char c : dirs.toCharArray()) {
                if (c == 'N') {
                    addEdge(NS,s1, s2);  //不要忘了把两个node都加到graph里
                } else if (c == 'S') {
                    addEdge(NS, s2, s1);
                } else if (c == 'E') {
                    addEdge(EW, s1, s2);
                } else if (c == 'W') {
                    addEdge(EW, s2, s1);
                }
            }
        }
        // topological order
        if (topoOrder(NS) == false ||topoOrder(EW) == false) {
            return false;
        }
        // if we could run topologcai order ==> no cycle
        return true;
    }
    // if graph has topological order, return true, else return false
    private boolean topoOrder(Map<String, Set<String>> map) {
        Map<String, Integer> marked = new HashMap<>();
        // initialize marked map
        for (String key : map.keySet()) {
            marked.put(key, 0);
        }
        for (String key :map.keySet()) {
            if (dfs(key, map, marked) == false) return false;
        }
        // we can find a topological order
        return true;
    }
    private boolean dfs(String key, Map<String, Set<String>> map, Map<String, Integer> marked) {
         Integer mark = marked.get(key);
         if (mark == 2) return true;
         if (mark == 1) return false;

         marked.put(key, 1);
         for (String next : map.get(key)) {
             if (!dfs(next, map, marked)) return false;
         }
         marked.put(key, 2);
         return true;
    }
    // add one directed edge start from v1 to v2 , and add node
    private void addEdge(Map<String, Set<String>> map, String v1, String v2) {
        if (map.get(v1) == null) map.put(v1, new HashSet<>());
        map.get(v1).add(v2);
        if (!map.containsKey((v2))) map.put(v2, new HashSet<>());
    }
    public static void main(String[] args) {
        DirValidator validator = new DirValidator();
        System.out.println(validator.validate(new String[]{"A N C", "A NW C", "A S C"}));
    }
    private void printGraph(Map<String, Set<String>> map) {
        for (String key : map.keySet()) {
            System.out.printf("start: %s to ", key);
            for (String str : map.get(key)) {
                System.out.printf("%s ", str);
            }
            System.out.println();
        }
    }
}

```