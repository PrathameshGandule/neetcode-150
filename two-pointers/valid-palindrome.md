# Valid palindrome
# Date 24-01-2026
# Problem link
- https://leetcode.com/problems/valid-palindrome/description/
# Description
- We are given string contaning alphabets, numbers, and other symbols like punctuation, space, non-alphanumeric chars etc.
- we have to determine if the string is a valid **palindrome** or not after removing all non-alphanumeric chars
- Example
```bash
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
```
# Approach 1 - `clean, reverse and compare`
- In this approach we first clean the strings of all other non-alphanumeric chars
- then we simply create a reverse of that string
- then we return the comparison of them as an output
```cpp
class Solution {
public:
    bool isPalindrome(string s) {
        string rev = "";
        string clean = "";
        int n = s.length();
		// cleaning the input string
        for(int i=0 ; i<n ; i++){
			// skip the char if it's not a alpha or num
            if(!isalnum(s[i])) continue;
			// convert the char to lower case and add to new string
            clean += tolower(s[i]);
        }
        int cn = clean.length();
		// create a reverse from new clean string
		// another way to reverse
		/*	string rev = clean;
		*	reverse(rev.begin(), rev.end());
		*/
        for(int i=cn-1 ; i>=0 ; i--){
            rev += clean[i];
        }
		// compare them
        return rev == clean;
    }
};
```
- Time complexity
  - activity = n + n
  - `O(n)` as only iterate in single loop
- Space complexity
  - activity = n + n
  - `O(n)` as we have to store the reverse num and clean string from the input string

# Approach 2 - two pointers
- Here we take two pointers `l=0` and `r=n-1`
- then we iterate over the string from both sides while `l<r`
- if current char with l or r is non-alphanumeric we skip it and go ahead
- else we compare the lowercase versions of current `s[l]` and `s[r]`
- if not same return `false`
- else at the end return `true`
```cpp
class Solution {
public:
    bool isPalindrome(string s) {
        int l=0, r=s.length()-1;
        while(l < r){
            if(!isalnum(s[l])){
                l++;
                continue;
            }
            if(!isalnum(s[r])){
                r--;
                continue;
            }
            if(tolower(s[l]) != tolower(s[r])){
                return false;
            }
            l++;
            r--;
        }
        return true;
    }
};
```
- Time complexity : O(n)
- Space complexity : O(1)

# Quick intuition/solution for the problem
- Use of two pointers for palindrome is good, and going only halfway through the iteration
***