```
You are given an array of strings words and a string chars.

A string is good if it can be formed by characters from chars (each character can only be used once).

Return the sum of lengths of all good strings in words.

 

Example 1:

Input: words = ["cat","bt","hat","tree"], chars = "atach"
Output: 6
Explanation: The strings that can be formed are "cat" and "hat" so the answer is 3 + 3 = 6.
Example 2:

Input: words = ["hello","world","leetcode"], chars = "welldonehoneyr"
Output: 10
Explanation: The strings that can be formed are "hello" and "world" so the answer is 5 + 5 = 10.
 

Constraints:

1 <= words.length <= 1000
1 <= words[i].length, chars.length <= 100
words[i] and chars consist of lowercase English letters.
```

```cpp
class Solution {
public:

 bool canForm ( string& str, int* arr ){
 int count[26] = {0} ; //function to check if our string contain all the character in less or equal frequency than of chars string given.
 for(auto character: str){
    count[character-'a']++ ;
}

for(auto character : str){
    if(count[character-'a'] > arr[character-'a'] )
    return false ; // if our string contain more frequency of any character , then it can't be made from chars string , hence return false /
}
return true ;
}

    int countCharacters(vector<string>& words, string chars) {
        int arr[26] = {0} ;
        for(auto character : chars){
            arr[character-'a']++ ;
        }

         int res = 0 ;
        // for(auto str : words){
        //     bool flag = 1;
        //     for(auto character : str){
        //         if(arr[character-'a'] == 0){
        //             flag = 0 ;
        //             break ;
        //         }
          
        //         }
        //               if(flag){
        //             res += str.size() ;
        //     }
        // }

        // return res ;
        

        for(auto str : words){
            if(canForm(str,arr)){
                res += str.size() ;
            }
        }

        return res ;
    }
};
```
