# Problem
A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

# Solution 1. 
try every solution and count, but it is too slow 
```
class Solution {
    private int count = 0;
    public int uniquePaths(int m, int n) {
        if(m == 1 && n == 1)
            return 1;
        // start at 1, 1
        findPath(2, 1, m, n);
        findPath(1, 2, m, n);
        return count;
    }
    
    private void findPath(int x, int y, int m, int n) {
        if(x == m && y == n) {
            count++;
            return;
        }
        // System.out.println(x+"*****"+y);
        if(x < m) {
            findPath(x+1, y, m, n);
        }
        if(y < n) {
            findPath(x, y+1, m, n);
        }
        
    }
}
```
