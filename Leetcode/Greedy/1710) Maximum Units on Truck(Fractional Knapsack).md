```
You are assigned to put some amount of boxes onto one truck. You are given a 2D array boxTypes, where boxTypes[i] = [numberOfBoxesi, numberOfUnitsPerBoxi]:

numberOfBoxesi is the number of boxes of type i.
numberOfUnitsPerBoxi is the number of units in each box of the type i.
You are also given an integer truckSize, which is the maximum number of boxes that can be put on the truck. You can choose any boxes to put on the truck as long as the number of boxes does not exceed truckSize.

Return the maximum total number of units that can be put on the truck.

 

Example 1:

Input: boxTypes = [[1,3],[2,2],[3,1]], truckSize = 4
Output: 8
Explanation: There are:
- 1 box of the first type that contains 3 units.
- 2 boxes of the second type that contain 2 units each.
- 3 boxes of the third type that contain 1 unit each.
You can take all the boxes of the first and second types, and one box of the third type.
The total number of units will be = (1 * 3) + (2 * 2) + (1 * 1) = 8.
Example 2:

Input: boxTypes = [[5,10],[2,5],[4,7],[3,9]], truckSize = 10
Output: 91
```

```Simple Trick : -
What you need in comparator function , just return that. you will get that.
For eg. -
In below code, you need to sort the 2d vector in descending order according to 2nd column
so you return v1[1] > v2[1] .
It means when comparing two vectors v1, v2. Sort them in descending order according to their 2nd value.
where v1 = 3,5     v2 = 7, 9
```
```sort function takes static comparator function only , gives error for non-static```
```cpp
class Solution {
public:
static bool cmp(vector<int> v1, vector<int> v2){
    return v1[1] > v2[1] ;
}

    int maximumUnits(vector<vector<int>>& boxTypes, int truckSize) {
        sort(boxTypes.begin(), boxTypes.end(), cmp) ;
        int res = 0 ;
        for(auto vec: boxTypes){
            if(vec[0] <= truckSize){
                truckSize -= vec[0] ;
                res = res + vec[0]*vec[1] ;
            }
            else{
                res = res + truckSize*vec[1] ;
                break;
            }
        }

        return res ;
    }
};
```
