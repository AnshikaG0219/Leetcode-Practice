## 520. Detect Capital
We define the usage of capitals in a word to be right when one of the following cases holds:

All letters in this word are capitals, like "USA".
All letters in this word are not capitals, like "leetcode".
Only the first letter in this word is capital, like "Google".
Given a string word, return true if the usage of capitals in it is right.

 

Example 1:
```
Input: word = "USA"
Output: true
```
Example 2:
```
Input: word = "FlaG"
Output: false
```

## Thought Process
- There are two cases based on first letter.
- First letter can be either capital or small.
- If it is small, then rest of the letters should be small, else it is wrong case.
- If it is capital, then we can look for 2nd letter.
- If 2nd letter is small, rest should be small.
- If 2nd letter is capital, rest should be capital.
```cpp
class Solution {
public:
    bool isCap(char c)
    {
        return c >= 'A' && c <= 'Z';
    }

    bool isSmallCheck(string word, bool is_small)
    {
        for(int i = 2; i < word.size(); i++)
        {
            //it should be small but is capital
            if(is_small && isCap(word[i])) return false;
            
            // it should be capital, but is not
            else if(!is_small && !isCap(word[i])) return false;
        }
        return true;
    }

    bool detectCapitalUse(string word) {
        bool is_first_capital = isCap(word[0]);

        //if first letter is small and any other letter is capital
        if(!is_first_capital)
        {
            for(int i = 1; i < word.size(); i++)
            {
                if(isCap(word[i])) return false;
            }
        }
        
        if(word.size() <= 2) return true;

        bool is_small = !isCap(word[1]);

        return isSmallCheck(word, is_small);
    }
};
```

## 2nd
- Calculate number of capital and lower letters.
- If all letters are capital or lower or only first is capital, then true.
- Else false.

```cpp
class Solution {
public:
    bool isCap(char c)
    {
        return c >= 'A' && c <= 'Z';
    }

    bool detectCapitalUse(string word) {
        int cap = 0;
        int lower = 0;
        int size = word.length();

        for(char c : word)
        {
            if(isCap(c)) cap++;
            else lower++;
        }

        if(cap == size || lower == size || (isCap(word[0]) && lower == size - 1)) return true;
        return false;
    }
};
```
