```
Assume you are an awesome parent and want to give your children some cookies. But, you should give each child at most one cookie.

Each child i has a greed factor g[i], which is the minimum size of a cookie that the child will be content with; and each cookie j has a size s[j]. If s[j] >= g[i], we can assign the cookie j to the child i, and the child i will be content. Your goal is to maximize the number of your content children and output the maximum number.

 

Example 1:

Input: g = [1,2,3], s = [1,1]
Output: 1
Explanation: You have 3 children and 2 cookies. The greed factors of 3 children are 1, 2, 3. 
And even though you have 2 cookies, since their size is both 1, you could only make the child whose greed factor is 1 content.
You need to output 1.
Example 2:

Input: g = [1,2], s = [1,2,3]
Output: 2
Explanation: You have 2 children and 3 cookies. The greed factors of 2 children are 1, 2. 
You have 3 cookies and their sizes are big enough to gratify all of the children, 
You need to output 2.
 

Constraints:

1 <= g.length <= 3 * 104
0 <= s.length <= 3 * 104
1 <= g[i], s[j] <= 231 - 1
```

```cpp
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        sort(s.begin(),s.end()) ;
        sort(g.begin(),g.end()) ;
        int res = 0 ;
        int m = g.size() - 1;
        int n = s.size() - 1;
        
// why are we sorting because we'll use greedy strategy....
// how greedy strategy ensure only 
//see , you need to content maximum number of children, it could only be possible when each one of the student who is getting the cookie will get the cookie near to his greed. because this way, each cookie size and student greed who both are compatible will ensure that maximum number of students will get the cookies means maximum number of student will be content.
// so how would you do that, just start from the student of lowest greed and simultaneously start with a cookie of lowest size, if the current cookie size is well enough that it can satisfy the greed of that student then assign that cookie to him & move to next student and next cookie simultaneously.

// now suppose if you have two student a-70 , b-40 and two cookies c1- 100 , c2 10 , let us say you alott b student of greed 40 with c1 cookie, but then a will not get any cookie because c2 size is just 10 , it can't satisfy the greed of student a of greed 70. 

// so , if you walk greedely , and you would say let us start with minimum to minimum first and then next with next .

// so you can say, sorting required for applying greedyness here.
    

        int i= 0 , j = 0 ;
        while(i <= m && j <= n){
            if(g[i] <=  s[j]){
                res++ ;
                i++ ;
                j++;
            }
            else{
                j++ ;
            }
        }

        return res ;
    }
};
```
