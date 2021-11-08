
![picture 12](https://i.loli.net/2021/10/13/oIaxVZ4XfKyzFlr.png)  
- 找最多的overlapping intervals


```java
/**
 * Definition of Interval:
 * public classs Interval {
 *     int start, end;
 *     Interval(int start, int end) {
 *         this.start = start;
 *         this.end = end;
 *     }
 * }
 */
class Point {
        int time;
        int flag;
        Point(int time, int flag) {
            this.time = time;
            this.flag = flag;
        }
        public static Comparator<Point> PointComparator = new Comparator<Point>(){
            @Override
            public int compare(Point p1, Point p2) {
                if (p1.time == p2.time) return p1.flag - p2.flag;
                else return p1.time - p2.time;
            }
        };
}
public class Solution {
    /**
     * @param airplanes: An interval array
     * @return: Count of airplanes are in the sky.
     */
    public int countOfAirplanes(List<Interval> airplanes) {
        // sweep line扫描线法
        List<Point> list = new ArrayList<>();
        for (Interval i : airplanes) {
            list.add(new Point(i.start, 1));  //起飞时间
            list.add(new Point(i.end, 0));  // 这里可以将飞机降落vlaue设置为-1更简单
        }
        
        Collections.sort(list, Point.PointComparator);

        // 进行扫描
        int cnt = 0;
        int ret = 0;
        for (Point p :list) {
            if (p.flag == 1) cnt++;  //起飞
            else cnt--;  //降落
            ret = Math.max(ret, cnt);
        }
        return ret;
    }


}
```