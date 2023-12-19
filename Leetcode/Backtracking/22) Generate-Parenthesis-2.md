//solely based on recursion, no back-tracking concept used.
/* main concept -->
Passing empty string in starting....

![image](https://github.com/HIMANSHU73/DataStructures_and_Algorithms/assets/78476814/66448c38-5231-4030-928e-9a82f5391f95)


```cpp

class Solution {
public:


 
  
  void backtrack(int open, int close, int n, string str,vector<string>& ans){
    
      if(open == n && close == n){ //base case 
          ans.push_back(str) ;
          return ;
      }
       
         if(open < n){
          // str = str + "(" ;
              backtrack(open+1,close,n,str+"(",ans) ;
          }
          
          if(open > close){
              //str = str + ")" ;
              backtrack(open,close+1,n,str+")",ans) ;
          }
      }  




    vector<string> generateParenthesis(int n) {
  
        vector<string> ans ;
                 backtrack(0,0,n,"",ans) ;
                 return ans ;
    }
};
```
