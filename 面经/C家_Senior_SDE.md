
```
Question:
Suppose you are building a library and have following definition of a function and two methods register and findMatches.
Register method registers a function and its argumentTypes in the library and findMatches accepts an input argument list and tries to find all the functions that match this input argument list.


Note:
If a function is marked as isVariadic=true, then the last argument can occur one or more number of times.

Example:
FuncA: [String, Integer, Integer]; isVariadic = false
FuncB: [String, Integer]; isVariadic = true
FuncC: [Integer]; isVariadic = true
FuncD: [Integer, Integer]; isVariadic = true
FuncE: [Integer, Integer, Integer]; isVariadic = false
FuncF: [String]; isVariadic = false
FuncG: [Integer]; isVariadic = false

findMatches({String}) -> [FuncF]
findMatches({Integer}) -> [FuncC, FuncG]
findMatches({Integer, Integer, Integer, Integer}) -> [FuncC, FuncD]
findMatches({Integer, Integer, Integer}) -> [FuncC, FuncD, FuncE]
findMatches({String, Integer, Integer, Integer}) -> [FuncB]
findMatches({String, Integer, Integer}) -> [FuncA, FuncB]

What is an optimal solution for this?
I could only think of Bruter Force approach.
Please help. Thank you :)
```

```java
import java.util.*;

public class Function {
    String name;
    List<String> argumentTypes;
    boolean isVariadic;

    public Function(String name, List<String> argumentTypes, boolean isVariadic) {
        this.name = name;
        this.argumentTypes = argumentTypes;
        this.isVariadic = isVariadic;
    }
}

class FunctionLibrary {
    public void register(Set<Function> functionSet) {
        // implement this method
    }
    public List<Function> findMatches(List<String> argumentTypes) {
        // implement this method
        return null;
    }
}

```


