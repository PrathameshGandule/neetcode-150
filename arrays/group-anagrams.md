# Group Anagrams
# Date 20-01-2026
# Problem link
- https://leetcode.com/problems/group-anagrams/description/
# Description
- Given a array of string, we have to group the strings which are anagrams and return a array of array where inner array consists of anagrams
- Example
```bash
Input: strs = ["eat","tea","tan","ate","nat","bat"]

Output: [["bat"],["nat","tan"],["ate","eat","tea"]]

Explanation:

There is no string in strs that can be rearranged to form "bat".
The strings "nat" and "tan" are anagrams as they can be rearranged to form each other.
The strings "ate", "eat", and "tea" are anagrams as they can be rearranged to form each other.
```
# Approach 1
- create a `unordered_map<string, vector<string>>`
- we iterate over the `strs` vector and sort the each string
- then we push back the current string for that sorted key
- since anagrams when sorted are same, each time we sort and push the current string in umap, we group the anagrams under one key
- then we iterate over this umap and simply push this grouped string in another vector
```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> umap;
        int n = strs.size();
        for(int i=0 ; i<n ; i++){
            string key = strs[i];
            sort(key.begin(), key.end());
            umap[key].push_back(strs[i]);
        }
        vector<vector<string>> res;
        for(auto ele : umap){
            res.push_back(ele.second);
        }
        return res;
    }
};
```
- Time complexity : O(n)
- Space complexity : O(n)
- Good solution but we need to sort everytime
- ANOTHER THING
- I did something similar on my own first but it was little different and repetitive
```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<int>> umap;
        vector<string> copyvec(strs.begin(), strs.end());
        int n = strs.size();
        for(int i=0 ; i<n ; i++){
            sort(copyvec[i].begin(), copyvec[i].end());
            umap[copyvec[i]].push_back(i);
        }
        vector<vector<string>> res;
        int cnt = 0;
        for(auto ele : umap){
            res.push_back({});
            for(auto num : ele.second){
                res[cnt].push_back(strs[num]);
            }
            cnt++;
        }
        return res;
    }
};
```
- Here I made extra `vector<string>` which was just a copy and pushed only the indexes of similar strings in umap
- and then again iterate over the umap in nested loop to push_back all the strs using these indexes 

# Approach 2
- Rather than sorting and storing anagrams for that string, we'll be constructing a key based on ascii values and push strings for that key in umap
- We create a `unordered_map<string, vector<string>>` and `vector<int> vec(26, 0)` 
- then we iterate over tha array of strs then increment the placeholder value for that char in curr string
- this created a vector of length 26. where chars which are present are incremented with their count in that
- then we iterate over this vector and create a string which is concatenation of it's values which are comma separated like `0,0,2,1,0,1,....,`
- now we push current string for this key
- here the principle is that anagrams will produce the same key, so they will fall in same bucket of strings
- then we just push these vectors in 2d vector of vectors as answer
```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> umap;
        int n = strs.size();
        string tempStr = "";
        vector<int> temp(26, 0);
        for(int i=0 ; i<n ; i++){
            for(char c : strs[i]){
                temp[c - 'a']++;
            }
            for(int j=0 ; j<26;  j++){
                tempStr += to_string(temp[j])+",";
            }
            umap[tempStr].push_back(strs[i]);
            tempStr = "";
            fill(temp.begin(), temp.end(), 0);
        }
        vector<vector<string>> res;
        for(auto ele : umap){
            res.push_back(ele.second);
        }
        return res;
    }
};
```
Time complexity : O(n)
Space complexity : O(n)
***