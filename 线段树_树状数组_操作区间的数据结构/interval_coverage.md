- 这题其实就是 56. merge intervals

![picture 3](https://i.loli.net/2021/10/28/MdgaVIXYD9n75TF.png)  


- naitve solution:  1. sorted by start 2. scan from left to right

```java
    public int[][] merge(int[][] intervals) {
        // naive solution, sort by start
        // sanity check        
        Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
        int[][] ret = new int[intervals.length][2];
        int index = 0;
        
        ret[index] = intervals[0];
        
        
        for (int i = 1; i < intervals.length; i++) {
            if (ret[index][1] >= intervals[i][0]) {   //不要忘了等于的情况
                ret[index][1] = Math.max(ret[index][1], intervals[i][1]);
            } else {
                index++;
                ret[index] = intervals[i];
            }
        }
        return Arrays.copyOf(ret, index + 1);
    }
```

- solution 2: segment tree

```java
class‌ ‌SegmentTreeNode‌ ‌{‌ ‌
    int‌ ‌start;‌ ‌
    int‌ ‌end;‌  ‌//‌ ‌[start,‌ ‌end]‌ ‌->‌ ‌[start,‌ ‌end‌ ‌+‌ ‌1)‌  这个表示的是连续区间‌
    int‌ ‌‌covered‌;‌  ‌//‌ ‌total‌ ‌length‌ ‌covered‌ ‌by‌ ‌the‌ ‌paint‌   这个属性等同于前面的sum,基本上把left child和right child的covered aggregate起来‌
    int‌ ‌count;‌      ‌//‌ ‌how‌ ‌many‌ ‌times‌ ‌this‌ ‌interval‌ ‌is‌ ‌covered‌ ‌
    SegmentTreeNode‌ ‌left,‌ ‌right;‌ ‌
}‌ ‌
 ‌
class‌ ‌IntervalCoverage‌ ‌{‌ ‌
    SegmentTreeNode‌ ‌root;‌

    // constructor
    public‌ ‌IntervalCoverage(int‌ ‌len)‌ ‌{‌ ‌
      root‌ ‌=‌ ‌buildTree(0,‌ ‌len);‌ ‌    //build tree的时候初始值都是0
    }‌ ‌
    ‌
    public‌ ‌int‌ ‌queryRange(int‌ ‌left,‌ ‌int‌ ‌right)‌ ‌{‌ ‌
    ‌
    }‌ ‌
    ‌
    public‌ ‌void‌ ‌add(int‌ ‌left,‌ ‌int‌ ‌right)‌ ‌{‌ ‌
      //‌ ‌interval‌ ‌[left,‌ ‌right]‌ ‌corresponds‌ ‌to‌ ‌subarray‌ ‌a[left,‌ ‌..,‌ ‌right‌ ‌-‌ ‌1]‌ ‌
       updateHelper(root,‌ ‌left,‌ ‌‌right‌ ‌-‌ ‌1,‌ ‌1‌);‌ ‌
    }‌ ‌
    ‌
    public‌ ‌void‌ ‌remove(int‌ ‌left,‌ ‌int‌ ‌right)‌ ‌{‌ ‌
       updateHelper(root,‌ ‌left,‌ ‌‌right‌ ‌-‌ ‌1,‌ ‌-1‌);‌ ‌
    }‌ ‌
    ‌
    private‌ ‌void‌ ‌updateHelper(SegmentTreeNode‌ ‌root,‌ ‌int‌ ‌left,‌ ‌int‌ ‌right,‌ ‌‌int‌ ‌diff‌)‌ ‌{‌ ‌
        if‌ ‌(root‌ ‌==‌ ‌null)‌ ‌return;‌ ‌
        //‌ ‌base‌ ‌case‌ ‌
        //‌ ‌if‌ ‌(left‌ ‌==‌ ‌root.start‌ ‌&&‌ ‌right‌ ‌==‌ ‌root.end)‌ ‌{‌ ‌
        if‌ ‌(left‌ ‌<=‌ ‌root.start‌ ‌&&‌ ‌root.end‌ ‌<=‌ ‌right)‌ ‌{‌ ‌
                root.count‌ ‌+=‌ ‌diff;‌ ‌
            //‌ ‌root.covered‌ ‌=‌ ‌?‌ ‌
            if‌ ‌(root.count‌ ‌==‌ ‌0)‌ ‌{‌ ‌
                ‌//‌ ‌‌root.covered‌ ‌=‌ ‌root.left.covered‌ ‌+‌ ‌root.right.covered;‌ ‌
                root.covered‌ ‌=‌ ‌‌root.start‌ ‌==‌ ‌root.end‌‌ ‌?‌ ‌0‌ ‌:‌ ‌root.left.covered‌ ‌+‌ ‌root.right.covered;‌ ‌
            }‌ ‌else‌ ‌{‌ ‌
            //‌ ‌be‌ ‌careful‌ ‌with‌ ‌+1,‌ ‌e.g.‌ ‌[0,‌ ‌4]‌ ‌actually‌ ‌represent‌ ‌[0,‌ ‌5)‌ ‌
                root.covered‌ ‌=‌ ‌root.end‌ ‌-‌ ‌root.start‌ ‌+‌ ‌1;‌ ‌
            }‌ ‌
            return;‌ ‌
        }‌ ‌
    ‌
        int‌ ‌mid‌ ‌=‌ ‌root.start‌ ‌+‌ ‌(root.end‌ ‌-‌ ‌root.start)‌ ‌/‌ ‌2;‌ ‌
        if‌ ‌(right‌ ‌<=‌ ‌mid)‌ ‌{‌ ‌
           updateHelper(root.left,‌ ‌left,‌ ‌right,‌ ‌diff);‌ ‌
        }‌ ‌else‌ ‌if‌ ‌(left‌ ‌>‌ ‌mid)‌ ‌{‌ ‌
           updateHelper(root.right,‌ ‌left,‌ ‌right,‌ ‌diff);‌ ‌
        }‌ ‌else‌ ‌{‌ ‌
          updateHelper(root,‌‌ ‌left,‌ ‌mid‌,‌ ‌diff);‌ ‌
          updateHelper(root,‌‌ ‌mid‌ ‌+‌ ‌1,‌ ‌right‌,‌ ‌diff);‌ ‌
        }‌ ‌
        ‌
        /*‌ ‌
        if‌ ‌(left‌ ‌<=‌ ‌mid)‌ ‌{‌ ‌
        updateHelper(root.left,‌ ‌left,‌ ‌right,‌ ‌diff);‌ ‌
        }‌ ‌
        if‌ ‌(right‌ ‌>‌ ‌mid)‌ ‌{‌ ‌
        297‌ ‌
        updateHelper(root.right,‌ ‌left,‌ ‌right,‌ ‌diff);‌ ‌
        }‌ ‌
        */‌ ‌
        ‌
        if‌ ‌(root.count‌ ‌==‌ ‌0)‌ ‌{‌ ‌
            root.covered‌ ‌=‌ ‌root.left.covered‌ ‌+‌ ‌root.right.covered;‌ ‌
        }‌ ‌else‌ ‌{‌ ‌
             root.covered‌ ‌=‌ ‌root.end‌ ‌-‌ ‌root.start‌ ‌+‌ ‌1;‌ ‌
        }‌ ‌
    }‌ ‌
}‌ 
```

add:‌ ‌O(log‌ ‌n)‌ ‌
remove:‌ ‌O(log‌ ‌n)‌ ‌
query:‌ ‌O(log‌ ‌n)‌ ‌
 ‌
space:‌ ‌O(n)‌ ‌
n‌ ‌is‌ ‌the‌ ‌max‌ ‌boundary‌ ‌of‌ ‌intervals.‌ ‌
What’s‌ ‌new‌ ‌here:‌ ‌
-how‌ ‌to‌ ‌represent‌ ‌‌intervals‌‌ ‌in‌ ‌Seg‌ ‌Tree‌ ‌
-how‌ ‌to‌ ‌deal‌ ‌with‌ ‌‌remove‌‌ ‌operation‌ ‌(add,‌ ‌query,‌ ‌build)‌ ‌
