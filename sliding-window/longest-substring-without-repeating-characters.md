# Longest Substring Without Repeating Characters
# Date 27-01-2026
# Problem link
- https://leetcode.com/problems/longest-substring-without-repeating-characters/description/
# Description
- Given a string s, find the length of the longest substring without duplicate characters.
- Example
```bash
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3. Note that "bca" and "cab" are also correct answers.
```
# Approach 1 - set
```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int n = s.length();
        if(n==0 || n==1) return n;
        unordered_set<char> uset;
        int maxlen = 0;
        int left = 0;
        for(int right=0 ; right<n ; right++){
            while(uset.find(s[right]) != uset.end()){
                uset.erase(s[left]);
                left++;
            }
            maxlen = max(maxlen, right-left+1);
            uset.insert(s[right]);
        }
        return maxlen;
    }
};
```