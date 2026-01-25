# Encode and Decode strings
# Date 20-01-2026
# Problem link
- https://neetcode.io/problems/string-encode-and-decode/question
- The leetcode problem link is behind paywall
# Description
- We are given 2 function to complete
- in `encode` function we have to encode a vector of strings into 1 string such that we will transfer it over the wire and we will be able to decode it on other side as same vector that we encoded
Example
```bash
Input: dummy_input = ["Hello","World"]

Output: ["Hello","World"]

Explanation:
Machine 1:
Codec encoder = new Codec();
String msg = encoder.encode(strs);
Machine 1 ---msg---> Machine 2

Machine 2:
Codec decoder = new Codec();
String[] strs = decoder.decode(msg);
``` 
# Approach 1 - `len|sep|str` method
- Now in this approach what we do is
- calculate length of current string then add a separator(any) like `#` then add the string and continue this pattern
```bash
["Hello", "World"]
encoded_str = "5#Hello5#World"
```
- Now by this logic we surely know that when to expect length of str and after where to start parsing for string and where to stop
- So if any character comes in they way, there will be no confusion to parse it
- My solution below which is little dangly and different
```cpp
class Solution {
public:

    string encode(vector<string>& strs) {
        string res = "";
        int len = 0;
        for(string str : strs){
            len = str.length();
            res += to_string(len)+'#'+str;
        }
        return res;
    }

    vector<string> decode(string s) {
        vector<string> res;
        int mode = 1;
        int tempLen = 0;
        string tempStr = "";
        int i=0;
        int n = s.length();
        while(i < n){
            if(mode == 1){
                while(s[i] != '#'){
                    tempLen = tempLen*10 + (s[i]-'0');
                    i++;
                }
                mode = 2;
                i++;
            }
            if(mode == 2){
                while(tempLen > 0){
                    tempStr += s[i];
                    i++;
                    tempLen--;
                }
                res.push_back(tempStr);
                tempStr = "";
                mode = 1;
            }
        }
        return res;
    }
};
```
- The solution from neetcode(little better and shorter)
```cpp
class Solution {
public:
    string encode(vector<string>& strs) {
        string res;
        for (const string& s : strs) {
            res += to_string(s.size()) + "#" + s;
        }
        return res;
    }

    vector<string> decode(string s) {
        vector<string> res;
        int i = 0;
        while (i < s.size()) {
            int j = i;
			// start looking for length part until '#' appears
            while (s[j] != '#') {
                j++;
            }
			// extract num part using substr(start, length) function and
			// convert to int using stoi function
            int length = stoi(s.substr(i, j - i));
            // go ahead of hash
			i = j + 1;
			// go ahead of whole string
            j = i + length;
			// pick up the string from ahead of hash upto that length
            res.push_back(s.substr(i, length));
			// now on to the next part on length for next str
            i = j;
        }
        return res;
    }
};
``` 
- Time complexity : O(m)
- Space complexity : O(m+n)
- `m` = sum of length of all strings and `n` = num of strs
***