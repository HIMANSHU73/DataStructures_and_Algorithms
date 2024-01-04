```Description```
```
You are given an integer array nums. You need to create a 2D array from nums satisfying the following conditions:

The 2D array should contain only the elements of the array nums.
Each row in the 2D array contains distinct integers.
The number of rows in the 2D array should be minimal.
Return the resulting array. If there are multiple answers, return any of them.

Note that the 2D array can have a different number of elements on each row.

 

Example 1:

Input: nums = [1,3,4,1,2,3,1]
Output: [[1,3,4,2],[1,3],[1]]
Explanation: We can create a 2D array that contains the following rows:
- 1,3,4,2
- 1,3
- 1
All elements of nums were used, and each row of the 2D array contains distinct integers, so it is a valid answer.
It can be shown that we cannot have less than 3 rows in a valid array.
Example 2:

Input: nums = [1,2,3,4]
Output: [[4,3,2,1]]
Explanation: All elements of the array are distinct, so we can keep all of them in the first row of the 2D array.
 

Constraints:

1 <= nums.length <= 200
1 <= nums[i] <= nums.length
```


```!st Solution```
```Time Complexity - O(n)  Space Complexity -  O(n)```
```cpp
class Solution {
public:
    vector<vector<int>> findMatrix(vector<int>& nums) {
   //most optimized solution 

   //why use hashmap ? when constraint says you have only elements upto the length of array nums
   //create an array of length nums.size()+1 , store frequency of all = 0.
   vector<int> freq(nums.size()+1,0) ;

   vector<vector<int>> res ;

//whenever you found a duplicate element again, create a new row into resultant array res, and then add that duplicate element into that new row.
   for(auto x : nums){
       if(freq[x] >= res.size()){
           res.push_back({}) ;
       }
       //each time you analyze that frequency of x is >= no. of rows in res, what would you need, you need an extra row to store that new duplicate element.
       //So, in above if block, you are doing the same thing.

       res[freq[x]].push_back(x) ; // add the element in required row.
       freq[x]++ ;// increase the count.
       //don't forget to dry-run.
   }

   return res ;
    
    }
};
```



```2nd, 3rd Solution```
```Time Complexity - O(n^2)  Space Complexity -  O(n)```

```cpp
class Solution {
public:
    vector<vector<int>> findMatrix(vector<int>& v) {
        unordered_map<int, int> um;
        for (auto &i : v){
            um[i]++;
        }
        vector<vector<int>> ans;
        while (!um.empty()) {
            vector<int> temp, toErase;
            for (auto &[f, s] : um) {
                temp.emplace_back(f);
                s--;
                if (s == 0)toErase.emplace_back(f); // here we are not erasing right here in traversal loop( why ?)
            } //Because erase function return iterator to next pointing element in flow which might skip some elements while we are traversing the map or it may point to some in-valid locaiton.
            ans.emplace_back(temp);
            for (auto &i : toErase){
                um.erase(i);
            }
        }
        return ans;
    }
};
```

/*---------------------------(SIMPLIFIED)-------------------------------

Made a frequency map to store number of occurance of all elements.
The most appearing elements count will decide the number of row in answer vector.
If we have a element appearing twice then will run a loop to push it in 2 rows, similarly done for all.
*/
```cpp
class Solution {
public:
    vector<vector<int>> findMatrix(vector<int>& nums) {
        unordered_map<int,int>mp;
        int cnt =0;

        for(auto a:nums){
            mp[a]++;
            cnt = max(cnt,mp[a]);
        }
        vector<vector<int>>v(cnt);
        for(auto a: mp){
            int num = a.first;
            int freq = a.second;

            for(int i =0;i<freq;i++){
                v[i].push_back(num);
            }
        }
        return v;
        
    }
};
```

```Extra Links```
Push_back vs emplace_back
https://medium.com/@its.me.siddh/modern-c-series-vector-push-back-or-emplace-back-e3a482ab4dcd

erase function in unordered_map or another containers
https://stackoverflow.com/questions/15662412/how-to-remove-multiple-items-from-unordered-map-while-iterating-over-it

https://www.appsloveworld.com/cplus/100/29/how-to-remove-multiple-items-from-unordered-map-while-iterating-over-it?expand_article=1
