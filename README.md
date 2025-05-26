# Hashing-1
Explain your approach in **three sentences only** at top of your code


## Problem 1:
Given an array of strings, group anagrams together.

Example:
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]

Note:
All inputs will be in lowercase.
The order of your output does not matter.

# Solution: I am sorting the word in the list, and using that as a key to build a hashmap
# where the value is a list with the grouped anagrams
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        hash_map = {}
        for index, word in enumerate(strs):
            key = ''.join(sorted(word)) 
            if key in hash_map:
                hash_map[key].append(word)
            else:
                hash_map[key] = [word]
        return list(hash_map.values())



## Problem 2:
Given two strings s and t, determine if they are isomorphic.
Two strings are isomorphic if the characters in s can be replaced to get t.
All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

Example 1:
Input: s = "egg", t = "add"
Output: true

Example 2:
Input: s = "foo", t = "bar"
Output: false

Example 3:
Input: s = "paper", t = "title"
Output: true
Note:
You may assume both s and t have the same length.


# Solution: I am using two mapping data structures to maintain mapping from s->t & t->s
# If an element already exists in the appropriate mapping structure, and has the same value, it passes the check. If it exists but is mapped to a different value, it fails. 
class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        
        s_to_t = {}
        t_to_s = {}
        
        for sc, tc in zip(s, t):
            if sc in s_to_t:
                if s_to_t[sc] != tc:
                    return False
            else:
                s_to_t[sc] = tc
            
            if tc in t_to_s:
                if t_to_s[tc] != sc:
                    return False
            else:
                t_to_s[tc] = sc
        
        return True


## Problem 3:
Given a pattern and a string str, find if str follows the same pattern.
Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in str.

Example 1:
Input: pattern = "abba", str = "dog cat cat dog"
Output: true

Example 2:
Input:pattern = "abba", str = "dog cat cat fish"
Output: false

Example 3:
Input: pattern = "aaaa", str = "dog cat cat dog"
Output: false

Example 4:
Input: pattern = "abba", str = "dog dog dog dog"
Output: false
Notes:
You may assume pattern contains only lowercase letters, and str contains lowercase letters that may be separated by a single space.

# Solution: Logic is identitical to problem 2 above
class Solution:
    def wordPattern(self, pattern: str, s: str) -> bool:
        words = s.split()

        if len(words) != len(pattern):
            return False
        
        char_to_word = {}
        word_to_char = {}

        for ch, word in zip(pattern, words):
            if ch in char_to_word:
                if char_to_word[ch] != word:
                    return False
            else:
                char_to_word[ch] = word
            
            if word in word_to_char:
                if word_to_char[word] != ch:
                    return False
            else:
                word_to_char[word] = ch
    
        return True
