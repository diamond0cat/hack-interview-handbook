1  2  3  4
2  5  1  3
3  1  2  4
5  4  3  1


这题能用pure recursion做吗？可以

starting from brute force:

step 1: brute force --> from all increasing paths, find the longest one

step 2:try to分解all the increasing paths
    longest = 0;
    for each (i, j):
        longest = max(longest, longest start from (i,j));


step 3: dp/recursion state: 

要看dependency graph里有没有cycle

