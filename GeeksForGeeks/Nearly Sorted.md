
# Ques
`Given an array of n elements, where each element is at most k away from its target position, you need to sort the array optimally.`

`Example 1:`

Input:
n = 7, k = 3
arr[] = {6,5,3,2,8,10,9}
Output: 2 3 5 6 8 9 10
Explanation: The sorted array will be
2 3 5 6 8 9 10

`Example 2:`

Input:
n = 5, k = 2
arr[] = {3,1,4,2,5}
Output: 1 2 3 4 5 

`Note: DO NOT use STL sort() function for this question.`

`Your Task:`
You are required to complete the method nearlySorted() which takes 3 arguments and returns the sorted array.

`Expected Time Complexity` : O(nlogk)

`Expected Auxilliary Space` : O(n)

`Constraints:`

1 ≤ n ≤ 10^6

1 ≤ k < n

1 ≤ arr[i] ≤ 10^7




`Explanation` :-->
```
We can sort the array which takes O(nlogn).
But, We have to use the fact that it's k-sorted. 
See the simple fact, array is k = 3 sorted in 1st example.

When you want to know who will come at 1st position ?, It means element that is going to come at 1st position will be atmost 3 distance away from current 1st element. or 
We can say The element which is going to come at 1st position will be out of first 4 elements. 
Similarly, the element which is going to come at 2nd position will be out of next 4 elements i.e. 1,2,3,4th index. 
And so on.......
```
_________________________________________________________________________________________________________________________________________________________
`Q) How to end ?`          ---
```
At last, there will be 3 elements in the priority-queue(min-heap) . You just empty it sequentially into res array. 
And res array will be sorted. 
Return this array.
```

`Q) How there will be 3 elements left in the array ?`
```
From starting what you are doing, you started from min-heap, taken element into it, extract one element , give it it's position & then insert new next element and place one correct
element at next position and so on.......
So, at last there will be 3 element and i (iterator in for loop) will be out of range. So, it will come out of for loop, and you will be having 3 elements remaining in min-heap.
```
_________________________________________________________________________________________________________________________________________________________



`Code -->`

```cpp
class Solution
{
    public:
    //Function to return the sorted array.
    vector <int> nearlySorted(int arr[], int num, int K){
   
        
        vector<int> res ;
        priority_queue<int, vector<int>, greater<int>> pq(arr, arr + K + 1) ; // priotiry-queue of first 4(k+1) elements, k = 3 in 1st example.
        
        for(int i = K + 1 ; i < num ; i++){
            res.push_back(pq.top()) ;
            pq.pop() ;
            pq.push(arr[i]) ;
        }
        
        while(!pq.empty()){
            res.push_back(pq.top()) ;
            pq.pop() ;
        }
        
        return res ;
    }
};
```


