```

661. Image Smoother

Description - 
An image smoother is a filter of the size 3 x 3 that can be applied to each cell of an image by rounding down the average of the cell and the eight surrounding cells (i.e., the average of the nine cells in the blue smoother). If one or more of the surrounding cells of a cell is not present, we do not consider it in the average (i.e., the average of the four cells in the red smoother).


Given an m x n integer matrix img representing the grayscale of an image, return the image after applying the smoother on each cell of it.

 

Example 1:


Input: img = [[1,1,1],[1,0,1],[1,1,1]]
Output: [[0,0,0],[0,0,0],[0,0,0]]
Explanation:
For the points (0,0), (0,2), (2,0), (2,2): floor(3/4) = floor(0.75) = 0
For the points (0,1), (1,0), (1,2), (2,1): floor(5/6) = floor(0.83333333) = 0
For the point (1,1): floor(8/9) = floor(0.88888889) = 0
Example 2:


Input: img = [[100,200,100],[200,50,200],[100,200,100]]
Output: [[137,141,137],[141,138,141],[137,141,137]]
Explanation:
For the points (0,0), (0,2), (2,0), (2,2): floor((100+200+200+50)/4) = floor(137.5) = 137
For the points (0,1), (1,0), (1,2), (2,1): floor((200+200+50+200+100+100)/6) = floor(141.666667) = 141
For the point (1,1): floor((50+200+200+200+200+100+100+100+100)/9) = floor(138.888889) = 138
 

Constraints:

m == img.length
n == img[i].length
1 <= m, n <= 200
0 <= img[i][j] <= 255
```

Solution : -

```cpp
class Solution {
public:
    vector<vector<int>> imageSmoother(vector<vector<int>>& img) {
       // we need to visit atmost 8 positions around a cell. 
       /* what we will do, we traverse on each cell, we'll go to all 8 neighbourhood cells.
        If cell is in range, we'll take the value of cell and store it in temp variable. 
       If cell is out of range, we skip that cell.
       && 
       We are counting the number of neighbourhood cells including itself in variable count.
       At last, temp = temp/count.   i.e. ,  dividing sum of values of neigbourhood by number of cells around it.
*/,
        int row[] = {-1 ,-1, -1, 0, 0, 1, 1, 1};
        int col[] = {-1 , 0, +1, -1, 1, -1, 0, 1}; 
        int m = img.size() ;
        int n = img[0].size() ;
        vector<vector<int>> res(m,vector<int>(n,0)) ;

        for(int i = 0 ; i < m ; i++){
            for(int j = 0 ; j < n ; j++){
                int temp = img[i][j] ; // variable used for storing the sum of all the neihbourhood cells including itself.
                int count = 1 ; // for counting the number of neighbouring cells.
                for(int k = 0 ; k < 8 ; k++){  // loop for adding the values of meighbourhood variables that are in range of matrix img.
                    if( (0 <= i+row[k] &&  i+row[k] < m)  && (0 <= j+col[k] && j+col[k] < n)){
                        temp += img[i+row[k]][j+col[k]] ;
                        count++ ;
                    }
                }
                temp = temp/count ; // calculating average 
                res[i][j] = temp ;  // storing the value in final matrix(resultant matrix.)
            }
        }

        return res ;// returning the matrix.
    }
};
```
