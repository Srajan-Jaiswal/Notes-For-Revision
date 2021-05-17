## Leetcode Imp questions based on Recursion and Backtracking 

Given an integer n, return all the numbers in the range [1, n] sorted in lexicographical order.
Example 1:

Input: n = 13
Output: [1,10,11,12,13,2,3,4,5,6,7,8,9]
Example 2:

Input: n = 2
Output: [1,2]
 

Constraints:

1 <= n <= 5 * 104
 

Follow up: Could you optimize your solution to use O(n) runtime and O(1) space?


```
class Solution {
public:
    vector<int> ans;
    void DFS(int idx, int n){
        if(idx>n) return;
        ans.push_back(idx);
        for(int i=0;i<10;i++){
            DFS(idx*10+i,n);
        }
    }
    vector<int> lexicalOrder(int n) {
        for(int i=1;i<10;i++){
            DFS(i,n); 
        }
        return ans;
    }
};

```