N家店面

```java
import java.util.*;
public class ParseCommand {
    static class Pair {
        String cmd;
        int num;
        public Pair(String cmd, int num) {
            this.cmd = cmd;
            this.num = num;
        }
    }
    private static void print(List<Pair> cmds) {
        for (Pair p :cmds) {
            System.out.print(p.cmd + ":" +p.num + ", ");
        }
        System.out.println();
    }
    public static void main(String[] args) {
        List<Pair> cmds = parse("Naa12S2E");
        print(cmds);
        System.out.println();
        cmds = parse("S12S2E102");
        print(cmds);
    }
    private static List<Pair> parse(String s) {
        char[] arr = s.toCharArray();
        StringBuilder sb = new StringBuilder();
        int count = 0;
        List<Pair> list = new ArrayList<>();
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] >= 'A' && arr[i] <= 'Z') {
                if (sb.length() != 0) {
                    String str = sb.toString();
                    count = count == 0 ? 1 : count;
                    list.add(new Pair(str, count));
                    sb.setLength(0);
                    count = 0;
                }
                sb.append(arr[i]);
            } else if (arr[i] >= 'a' && arr[i] <= 'z') {
                sb.append(arr[i]);
            } else if (arr[i] >= '0' && arr[i] <= '9'){
                count = count * 10 +(arr[i] - '0');
            }
        }
        if (sb.length() != 0) {
            count = count== 0 ? 1 : count;
            list.add(new Pair(sb.toString(), count));
        }
        return list;
    }
}
```




```java
// N, E, S, W, Ne, Nw, Brk, Acc
// Command := capital letter, 0 or more lowercase
// Count := 0 or more digits
// RepeatedCommand := Command and Count
// N2 Brk10
// “N2AccNe10Brk” --> { “N”: 2, “Acc”: 1, “Ne”: 10, “Brk”: 1}
// “[N2Acc]2” 
 //         s

// [N2Acc]2[NaaBcc]5 ==> "N2Acc":2, "NaaBcc":5 ==> {N: 4, Acc: 2}, {} 
// Nab
// N2AccNe10Brk 
/*   N2
     Acc
        Ne10
           Brk
 */  
 
 /*
 scan input string twice:  
 step 1: : scan from right to left to split input string into multiple segment which are commands group
       capital followed by 0 or more lower, may or may not following by 0 or more digits
 step 2: for each segment, scan from left to right to find each command in this segment
         N2AccNe10Brk 
                     s
         N2
           Acc:1
              Ne1*10 + 0
                  Brk
 */        

import java.io.*;
import java.util.*;
import java.text.*;
import java.math.*;
import java.util.regex.*;

public class Solution {
// N2AccNe10Brk    
    
// [N2Acc]2[NaaBcc]5 ==> "N2Acc":2, "NaaBcc":5 ==> {N: 4, Acc: 2}, {} 
// Nab
// N2AccNe10Brk 
  static Map<String, Integer> parseCommands(String s) {
      // sanity check
      Map<String, Integer> map = new HashMap<>();
      // ascii contiguous ==> c >= 'A' && c <= 'Z'
     
      char[] arr = s.toCharArray();
      // N2AccNe10Brk  
      // N
      // scan from left to right to split it
      StringBuilder sb = new StringBuilder();  // start a new segment
      int count = 0;
      for (int i = 0; i < arr.length; i++) {
          if (arr[i] >= 'A' && arr[i] <= 'Z') {
               sb = new StringBuilder();
               sb.append(arr[i]);
          } else if (arr[i] >= 'a' && arr[i] <= 'z') {
              sb.append(arr[i]);
          } else { // it is a digit
              String str = sb.toString();
              if (map.containsKey(str)) {
                  map.put(str, map.get(str) * 10 + arr[i]);
              } else {
                  map.put(str, arr[i]);
              }
              
          }
      }
      
      return map;
  }

 public static void main(String[] args) {


       // sum = parseCommands();
       // System.out.println(sum);
   }
}

```