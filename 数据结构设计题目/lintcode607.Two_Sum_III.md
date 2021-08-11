

```java
public class TwoSum {
    private Map<Integer, Integer> counter;
    
    public TwoSum() {
        counter = new HashMap<Integer, Integer>();
    }

    // Add the number to an internal data structure.
    public void add(int number) {
        counter.put(number, counter.getOrDefault(number, 0) + 1);
    }

    // Find if there exists any pair of numbers which sum is equal to the value.
    public boolean find(int value) {
        for (Integer num1 : counter.keySet()) {
            int num2 = value - num1;
            int desiredCount = num1 == num2 ? 2 : 1;
            if (counter.getOrDefault(num2, 0) >= desiredCount) {
                return true;
            }
        }
        return false;
    }
}

// Your TwoSum object will be instantiated and called as such:
// TwoSum twoSum = new TwoSum();
// twoSum.add(number);
// twoSum.find(value);
```