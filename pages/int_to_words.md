---
layout: post
author: Sreeraj
title: Convert Integer to English words
---


```cpp
class Solution {
public:
    vector<string> THOUSANDS={"", "Thousand", "Million", "Billion"};
    vector<string> TENS = {"", "Ten", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"};
    vector<string> ONES = {"", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten",
                          "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen"};
    string numberToWords(int num) {
        if(num == 0) return "Zero";
        int i = 0;
        string word = "";
        while(num > 0) {
            int digit = num%1000;
            num/=1000;
            string temp = helper(digit);
            if(digit!=0)
            word = std::regex_replace(temp, std::regex(" +$"), "") + " " + THOUSANDS[i] + " "+ word;
            i++;
        }
        return std::regex_replace(word, std::regex(" +$"), "");
    }
    
    string helper(int digit) {
        if(digit == 0)
            return "";
        else if(digit < 20)
            return ONES[digit];
        else if(digit < 100)
            return TENS[digit/10] + " " + helper(digit%10);
        else 
            return ONES[digit/100]+ " Hundred " +helper(digit%100);  
    }
    
};
```