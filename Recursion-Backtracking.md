## Leetcode Imp questions based on Recursion and Backtracking 


## Question 1  Lexographical Numbers

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



## Question 2.  Letter Tile Possibilities

You have n  tiles, where each tile has one letter tiles[i] printed on it.

Return the number of possible non-empty sequences of letters you can make using the letters printed on those tiles.

 

Example 1:

Input: tiles = "AAB"
Output: 8
Explanation: The possible sequences are "A", "B", "AA", "AB", "BA", "AAB", "ABA", "BAA".
Example 2:

Input: tiles = "AAABBC"
Output: 188


```

class Solution {
public:
    int cnt=0;
    unordered_set<string> st,sub_st;
    void find_permut(int l,int r,string tiles){
        if(l==r){
            st.insert(tiles);
        }
        for(int i=l;i<=r;i++){
        swap(tiles[l],tiles[i]);    
        find_permut(l+1,r,tiles);
        swap(tiles[l],tiles[i]);
        }
    }
    void find_subsets(int i,string in, string  out){
        if(i==in.length()){
            st.clear();
            if(sub_st.find(out) == sub_st.end() && out!=""){ 
            sub_st.insert(out);    
            find_permut(0,out.length()-1,out);
            //cout<<st.size()<<endl;
            cnt+=st.size();
            }
            return;
        }
        find_subsets(i+1,in,out+in[i]);
        find_subsets(i+1,in,out);    
    }
    
    int numTilePossibilities(string tiles) {
        sort(tiles.begin(),tiles.end()); // sorting is for avoiding subsets like (cd) (dc) 
        find_subsets(0,tiles,"");
        /*for(auto it:sub_st){
            cout<<it<<endl;
        }*/
        return  cnt;
    }
};


```





