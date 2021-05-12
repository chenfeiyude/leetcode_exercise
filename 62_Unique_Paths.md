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
        // start at 1, 1
        findPath(1, 1, m, n);
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

# Solution 2
if a point is already count, then no point try all the possibilities for the point again
```
class Solution {
    private int count = 0;
    public int uniquePaths(int m, int n) {
        // if(m == 1 && n == 1)
        //     return 1;
        // start at 1, 1
        int[][] pathArray = new int[m][n];
        
        return findPath(0, 0, m, n, pathArray);
    }
    
    private int findPath(int x, int y, int m, int n, int[][] pathArray) {
        if(x == m - 1 && y == n - 1) {
            pathArray[x][y] = 1;
            return pathArray[x][y];
        }
        if(pathArray[x][y] > 0)
            return pathArray[x][y];
        int count = 0;
        if(x + 1 < m) {
            count += findPath(x+1, y, m, n, pathArray);
        }
        if(y + 1 < n) {
            count += findPath(x, y+1, m, n, pathArray);
        }
        pathArray[x][y] = count;
        return pathArray[x][y];
    }
}
```
