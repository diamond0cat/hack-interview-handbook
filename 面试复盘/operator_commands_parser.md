

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