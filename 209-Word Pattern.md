## 290. Word Pattern
Given a pattern and a string s, find if s follows the same pattern.

Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in s.

 

Example 1:
```
Input: pattern = "abba", s = "dog cat cat dog"
Output: true
```
Example 2:
```
Input: pattern = "abba", s = "dog cat cat fish"
Output: false
```
Example 3:
```
Input: pattern = "aaaa", s = "dog cat cat dog"
Output: false
```

## Thought Process
- If `a = dog` and `b = cat` then `dog cat cat dog = abba`, hence true.
- If `a = dog` and `b = cat` then `dog cat cat fish != abba`, hence false.
- Chance the string **s** to vector of strings/words.
- Condition to check is **bijection** i.e., if for each character in pattern there exists a unique word in s and all the characters are mapped to each word in s (sizes are equal), then return true else false.
- Map char of pattern -> word in s.
- If positions of these characters and words are same then the pattern matches.


```cpp
class Solution {
public:
    void getWords(string s, vector<string> &words) {
        string word = "";
        for(char c : s)
        {
            if(c == ' ')
            {
                words.push_back(word);
                word = "";
            }
            else
            word += c;
        }
        words.push_back(word);
    }
    
    
    bool wordPattern(string pattern, string s) {
        vector<string> words;
        getWords(s, words);

        if(pattern.size() != words.size()) return false;
        
        unordered_map<string, vector<int>> map_s;
        unordered_map<char, vector<int>> map_p;
        
        for(int i = 0; i < words.size(); i++)
        {
            map_s[words[i]].push_back(i);
            map_p[pattern[i]].push_back(i);
        }
        
        for(int i = 0; i < words.size(); i++)
        {
            if(map_s[words[i]] != map_p[pattern[i]]) return false;
        }
        
        return true;
    }
};
```
