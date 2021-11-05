- naive solution: 枚举所有的subarray,求出max - min

```java
    public static int getSubarrayBaoli(int[] arr, int num) {
        // sanity check
        if (arr == null || arr.length == 0) return 0;
        int count = 0;

        //enumerate all subarray
        for (int l = 0; l < arr.length; l++) {
            // L..L, L...L+1, L...L+2, .....L.n-1
            for (int r = l; r < arr.length; r++) {
                // arr[l...r]
                int max;
                int min;

                for (int i = l; i <= r; i++) {

                }
                //max-min= ?
                //valid++
            }
        }
    }
```

- solution 2:  最优解 O(n)  ==> 如果一个子数组达标，那么它内部任何一个子数组都达标； 如果子数组不达标，那么它往左或往右扩的也不达标
- 对一个窗口做出一个最大值的更新结构，最大值的更新结构 ==> max更，min更，一个维护窗口最大值，一个维护窗口最小值



### 优化的几个思路：
### 1.数据状况能不能做优化
### 2.问题本身求的是什么：  这个题范围和问题本身建立了单调性(如果一个子数组达标，那么它内部任何一个子数组都达标； 如果子数组不达标，那么它往左或往右扩的也不达， 开头位置符合窗口的运动轨迹，结尾如果滑到不达标位置就可以停了，所以问题本身的单调性和窗口的滑动轨迹连接在了一起)



![picture 6](https://i.loli.net/2021/11/05/AThINVegGmtWbZY.png)  


```java
    // sliding window + 两个monotonic deque  ==> time = O(n)
    public static int getNum(int[] arr, int num) {
        // sanity check
        if (arr == null ||arr.length == 0) return 0;

        Deque<Integer> qmin = new LinkedList<>();
        Deque<Integer> qmax = new LinkedList<>();
        int l = 0, r = 0;  // [L, R)  左闭右开
        int res = 0;
        //[L, R-1] ==> 【L, R), R是第一个不达标的位置
        while (l < arr.length) {  //l是窗口的开头, 尝试每个开头，用滑动窗口的开头来分解所有的解
            // 如果此时窗口的开头是L,下面的while的工作： R向右扩到违规为止
            while (r < arr.length) {
                // 递增队列维护最小值
                while (!qmin.isEmpty() && arr[qmin.peekLast()] >= arr[r]) {
                    qmin.pollLast();
                }
                qmin.offerLast(r);
                // 递减队列维护最大值
                // R --> arr[R]
                while (!qmax.isEmpty() && arr[qmax.peekLast()] <= arr[r]) {
                    qmax.pollLast();
                }
                qmax.offerLast(r);

                if (arr[qmax.getFirst()] - arr[qmin.getFirst()] > num) {
                    // 窗口已经不达标了
                    break;
                }
                r++;
            }
            // r是达标位置的下一个位置 a.k.a.第一个违规的位置
            res += r - l;      //这里是左闭右开， R不包括在内
            // remove left, 过期的元素踢掉 
            if (qmin.peekFirst() == l) {
                qmin.pollFirst();
            }
            if (qmax.peekFirst() == l) {
                qmax.pollFirst();
            }
            l++;
        }
        return res;
    }
    ```


    ```java
    package class01;

import java.util.LinkedList;

public class Code02_AllLessNumSubArray {

	public static int getNum(int[] arr, int num) {
		if (arr == null || arr.length == 0) {
			return 0;
		}
		LinkedList<Integer> qmin = new LinkedList<Integer>();
		LinkedList<Integer> qmax = new LinkedList<Integer>();
		int L = 0;
		int R = 0;
		// [L..R) -> [0,0) 窗口内无数 [1,1)
		// [0,1) -> [0~0]
		int res = 0;
		while (L < arr.length) { // L是开头位置，尝试每一个开头

			// 如果此时窗口的开头是L,下面的while工作:R向右扩到违规为止

			while (R < arr.length) { // R是最后一个达标位置的再下一个
				while (!qmin.isEmpty() && arr[qmin.peekLast()] >= arr[R]) {
					qmin.pollLast();
				}
				qmin.addLast(R);
				// R -> arr[R],
				while (!qmax.isEmpty() && arr[qmax.peekLast()] <= arr[R]) {
					qmax.pollLast();
				}
				qmax.addLast(R);

				if (arr[qmax.getFirst()] - arr[qmin.getFirst()] > num) {
					break;
				}
				R++;
			}

			// R是最后一个达标位置的再下一个，第一个违规的位置
			res += R - L;

			if (qmin.peekFirst() == L) {
				qmin.pollFirst();
			}
			if (qmax.peekFirst() == L) {
				qmax.pollFirst();
			}

			L++;

		}
		return res;
	}

	// for test
	public static int[] getRandomArray(int len) {
		if (len < 0) {
			return null;
		}
		int[] arr = new int[len];
		for (int i = 0; i < len; i++) {
			arr[i] = (int) (Math.random() * 10);
		}
		return arr;
	}

	// for test
	public static void printArray(int[] arr) {
		if (arr != null) {
			for (int i = 0; i < arr.length; i++) {
				System.out.print(arr[i] + " ");
			}
			System.out.println();
		}
	}

	public static void main(String[] args) {
		int[] arr = getRandomArray(30);
		int num = 5;
		printArray(arr);
		System.out.println(getNum(arr, num));

	}

}
```