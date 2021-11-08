- 一定存在，global minimum一定是local minimum, local minimum不止一个

https://stackoverflow.com/questions/10063289/find-a-local-minimum-in-a-2-d-array

- The same problem is mentioned in web version of book Algorithms by Robert Sedgewick and Kevin Wayne. (See "Creative problems" section, problem 19).

    - The hint for the problem given by author in that link is:

        -  Find the minimum in row N/2, check neighbors p and q in column, if p or q is smaller then recur in that half.

        - A better aprroach would be : Find the minimum in row N/2, check all entries in its column, if we get smaller entry in column, then recur in the row where smaller column entry belongs.

-  eg. For array below, N=5:

- 1  12  3   1  -23  
* 7   9  8   5   6
* 4   5  6  -1  77
* 7   0  35 -2  -4
* 6  83  1   7  -6
* Step 1: The middle row is [4   5  6  -1  77]. ie. row number 3.  

* Step 2: Minimum entry in current row is -1.  找N/2 row中的最小值

* Step 3: Column neighbors for min entry (ie. -1) are 5 and -2. -2 being the minimum neighbor. Its in the 4th row.

* Continue with steps 2-3 till we get the local min.


EDIT:

For example mentioned in comment from @anuja (the main problem is for n-by-n array. This input is 3-by-4 array but we can work with that) :

```
1 2 3  4 
5 1 6 -1
7 3 4 -2

```

Step 1: The middle row is [5 1 6 -1]. ie. row number 2.

![20210803163719](https://i.loli.net/2021/08/04/QvXPgZ4CqI6FseR.png)

Step 2: Minimum entry in current row is -1.
![20210803163742](https://i.loli.net/2021/08/04/LEeXbt9daC6uPpB.png)

Step 3: Column neighbors for min entry (ie. -1) are 4 and -2. -2 is the minimum column neighbor. Its in the 3rd row.
![20210803163754](https://i.loli.net/2021/08/04/EfLRz4N1UOpoPMi.png)

Iterating to Step 2: -2 is smallest in its row and smallest amongst its column neighbours. So we end with -2 as output for local minimum.
![20210803163811](https://i.loli.net/2021/08/04/mKZVWQfvDcuH7rC.png)