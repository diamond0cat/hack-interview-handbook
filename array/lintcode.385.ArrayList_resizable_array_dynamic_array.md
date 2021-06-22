原题链接：
https://www.lintcode.com/problem/385/


 ```    
Description
Implement an ArrayListManager which can:

- create(n). Create an ArrayList of integers contains [0, 1, 2, ... n-1]
clone(list). 
- Clone a list. The cloned list should independent with the original list.
- get(list, index). Get the element on the index position of the list.
- set(list, index, val). Change the value the element of index position to given val.
- remove(list, index). Remove the element on the index position.
- indexOf(list, val). Find the first index of element that equals to val and return its index.
Please use the methods provided by ArrayList. See documents：ArrayList Document


```


```java

public class ArrayListManager {
    /**
     * @param n: You should generate an array list of n elements.
     * @return: The array list your just created.
     */
    public static ArrayList<Integer> create(int n) {
        // Write your code here
        ArrayList<Integer> list = new ArrayList<Integer>();
        for (int i = 0; i < n; i++) {
            list.add(i);
        }
        return list;
    }
    
    /**
     * @param list: The list you need to clone
     * @return: A deep copyed array list from the given list
     */
    public static ArrayList<Integer> clone(ArrayList<Integer> list) {
        // Write your code here
        ArrayList<Integer> dist = new ArrayList<Integer>();
        for (Integer a : list)
            dist.add(a);
        return dist;
        //return list;
    }
    
    /**
     * @param list: The array list to find the kth element
     * @param k: Find the kth element
     * @return: The kth element
     */
    public static int get(ArrayList<Integer> list, int k) {
        // Write your code here
        return list.get(k);
    }
    
    /**
     * @param list: The array list
     * @param k: Find the kth element, set it to val
     * @param val: Find the kth element, set it to val
     */
    public static void set(ArrayList<Integer> list, int k, int val) {
        // write your code here
        list.set(k, val);
    }
    
    /**
     * @param list: The array list to remove the kth element
     * @param k: Remove the kth element
     */
    public static void remove(ArrayList<Integer> list, int k) {
        // write tour code here
        list.remove(k);
    }
    
    /**
     * @param list: The array list.
     * @param val: Get the index of the first element that equals to val
     * @return: Return the index of that element
     */
    public static int indexOf(ArrayList<Integer> list, int val) {
        // Write your code here
        if (list == null)
            return -1;
        return list.indexOf(val);
    }
}


```

      
      



