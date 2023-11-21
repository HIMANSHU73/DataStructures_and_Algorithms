Q) 
```
Given an array of integers nums, sort the array in ascending order and return it.

You must solve the problem without using any built-in functions in O(nlog(n)) time complexity and with the smallest space complexity possible.

 

Example 1:

Input: nums = [5,2,3,1]
Output: [1,2,3,5]
Explanation: After sorting the array, the positions of some numbers are not changed (for example, 2 and 3), while the positions of other numbers are changed (for example, 1 and 5).
Example 2:

Input: nums = [5,1,1,2,0,0]
Output: [0,0,1,1,2,5]
Explanation: Note that the values of nums are not necessairly unique.
 

Constraints:

1 <= nums.length <= 5 * 104
-5 * 104 <= nums[i] <= 5 * 104
```
Solution)
```cpp
class Solution {
public:

void merge(vector<int>& nums,int l, int mid, int r){
    int n1 = mid - l + 1;
    int n2 = r - mid ;
    int i = 0 , j = 0 , k = l ;
    vector<int> left(n1) ;
    vector<int> right(n2) ;
    for(int m = 0 ; m < n1 ; m++){
        left[m] = nums[m+l] ;//storing left array into left.
    }
    for(int m = 0 ; m < n2 ; m++){
        right[m] = nums[m+mid+1] ;//storing right array into right.
    }

    //now merging them into nums & make that sort 
    while(i < n1 && j < n2){
        if(left[i] <= right[j]){
            nums[k] = left[i] ;
            i++ ;
            k++;
        }
        else{
            nums[k] = right[j] ;
            j++;
            k++;
        }
    }

    while(i < n1){
        nums[k] = left[i] ;
        i++ ;
        k++;
    }

    
    while(j < n2){
        nums[k] = right[j];
        j++ ;
        k++;
    }
}
void mergesort(vector<int>& nums, int l, int r){
    if(l < r){
        int mid = l + (r-l)/2 ;
        mergesort(nums,l,mid) ;
        mergesort(nums,mid+1,r) ;
        merge(nums,l,mid,r) ;
    }
}
    vector<int> sortArray(vector<int>& nums) {
        mergesort(nums,0,nums.size()-1) ;
        return nums ;
    }
};

```
