![image](https://github.com/HIMANSHU73/DataStructures_and_Algorithms/assets/78476814/f36fd8c3-aa09-44cb-8042-4ac50086d1ad)










class Solution {
public:
//initially open == 2 & close == 2 , when you consume these open and close, you decrease it by 1 
//Rest is in image.

void backtrack(string &s,int open,int close, vector<string>& ans){
    
    
    //base case
    if(open == 0 && close == 0){
        ans.push_back(s) ;
        return ;
    }
    
    if(open > 0){
        s.push_back('(') ;
        backtrack(s,open-1,close,ans) ;
        s.pop_back() ;  //backtrack.................
    }
    
    if(close > 0 && open < close){
        s.push_back(')') ;
        backtrack(s,open,close-1,ans) ;
        s.pop_back() ; //backtrack..................
    }
}

    vector<string> generateParenthesis(int n) {
        vector<string> ans ;
        string s;
        backtrack(s,n,n,ans) ; //initially open == 2 , close == 2
        return ans ;
    }
};
