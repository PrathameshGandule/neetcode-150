# Valid Anagram
# Date 19-01-2026
# Problem link
- https://leetcode.com/problems/valid-anagram/description/

# Description
- Given two strings s and t, return true if t is an anagram of s, and false otherwise.
- Example
```bash
Input: s = "anagram", t = "nagaram"
Output: true
```

# Approach 1 - `unordered map and inc & dec`
- If length of `s` and `t` is not same return false
- Create a `unordered_map<char, int>` and increment count for each found element in `s` string
- Then decrement the count found for each element in `t` string
- Then iterate over the map and see if any char's count is more than zero, if so return `false` else return `true` at end.
- ANOTHER METHOD COULD BE MAKING 2 UNORDERED_MAPS and counting for each string then comparing maps, would've taken unnecessary extra space 
```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        int slen = s.length();
        int tlen = t.length();
        if(slen != tlen) return false;
        unordered_map<char, int> umap;
        for(int i=0 ; i<slen ; i++){
			umap[s[i]]++;
        }
        for(int i=0 ; i<slen ; i++){
			umap[t[i]]--;
        }
        for(auto ele : umap){
			if(ele.second > 0) return false;
        }
        return true;
    }
};
```
- Time complexity : O(n)
- Spce complexity : O(n)

# Approach 2 - `ascii vector and inc & dec`
- If length of `s` and `t` is not same return false
- Make vector of size 26 (assuming all lowercase ascii chars only) initialized to 0
- Iterate over the `s` and `t` and increment and decrement respectively the count for that char in vector
- Then iterate over the vector and look for any non-zero count for a char, if found return `false`, else at the end return `true`
```cpp
class Solution {
	public:
    bool isAnagram(string s, string t) {
		int slen = s.length();
        int tlen = t.length();
        if(slen != tlen) return false;
        vector<int> cnt(26, 0);
        for(int i=0 ; i<slen ; i++){
			cnt[s[i] - 'a']++;
            cnt[t[i] - 'a']--;
        }
        for(int ele : cnt){
			if(ele != 0) return false;
        }
        return true;
    }
};
```
- Time complexity : O(n)
- Space complexity : O(26) ~ O(1)

# Approach 3 - `sort and compare`
- If length of `s` and `t` is not same return false
- Sort both the strings and return their comparison
```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        int slen = s.length();
        int tlen = t.length();
        if(slen != tlen) return false;
        sort(s.begin(), s.end());
        sort(t.begin(), t.end());
        return s == t;
    }
};
```
- Time complexity : O(n logn)
- Space complexity : (depands on sorting algorithm)
- Inefficient than other solutions
*** 