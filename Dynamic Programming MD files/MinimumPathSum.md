## Minimum Path Sum
### Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.<br/>

## Note: You can only move either down or right at any point in time.

```
Input:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
Output: 7
Explanation: Because the path 1→3→1→1→1 minimizes the sum.
```
## Explanation
### The only way to move to spot (r,c) is by moving to one of the adjacent spots: (r-1, c) or (r, c-1). So, we need to find a path to either (r-1, c) or (r, c-1) <br/>
### dp(row, col) = val[row][col]  + Math.min(dp(row-1, col), dp(row, col-1));

### <strong> Time Complexity: O(2<sup>(r+c)</sup>) </strong> <br/>

```
import java.util.*;
class MinimumPathSum {
    public int minPathSum(int[][] grid) {
        int row = grid.length - 1;
        int col = grid[0].length - 1;
        int[][] uniquePathSum = new int[row+1][col+1];
        for(int[] arrayRows : uniquePathSum){
            Arrays.fill(arrayRows, Integer.MAX_VALUE);
        }
       return findMinPath(row, col, uniquePathSum, grid);
        
    }
    
    public int findMinPath(int row, int col, int[][] uniquePathSum, int[][] grid){
       
        if(row < 0 || col < 0)
            return Integer.MAX_VALUE;
        if(row == 0 && col == 0){
            return grid[row][col];
        }
        if(uniquePathSum[row][col] != Integer.MAX_VALUE){
            return uniquePathSum[row][col];
        }
        else{
            uniquePathSum[row][col] = grid[row][col] + Math.min(findMinPath(row, col-1, uniquePathSum, grid), findMinPath(row-1, col, uniquePathSum, grid));
        }
        return uniquePathSum[row][col];
    }

    public static void main(String[] args){
        int[][] inputArray = {{1,3,1}, {1,5,1}, {4,2,1}};
        MinimumPathSum minSum = new MinimumPathSum();
        System.out.println(minSum.minPathSum(inputArray));
    }
}
```