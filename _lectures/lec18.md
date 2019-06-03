---
num: "lect18"
lecture_date: 2019-05-30
desc: 
ready: false
pdfurl: 
---
# Link to lecture slides
https://drive.google.com/drive/folders/1zP7YNmZXCYnAP8MrEiaf1Ov28ESpXR0s

# Recursion continued
To check if a recursive implementation is correct:
1. Each stopping case returns the correct value for that case
2. There's no infinite recursion
3. For the cases that involve recursion: if all recursive calls perform their actions correctly, then the entire case performs correctly

## Helper functions
Sometimes you may have a function that has an input parameter that's difficult to recurse on

If this is the case, sometimes it's easier to define a new function that takes in a different parameter (a.k.a a helper function)

The helper function performs the recursion, the parent function just calls (and maybe returns, depending on your use case) the helper function

# Binary search
So far we have done search using sequential search, where we iterate through a data structure (an array), and check if there are any elements present

If the data structure (an array) is already sorted, then we can use binary search

Here's how a binary search works:
1. We go to the center of the array, and we check if the value we want to search for is greater than, less than, or equal to the element we want to search
2. If it's equal, we immediately return the value
3. If it's greater than, we then find the middle element of the subarray right of the middle of the entire array
4. We do the same thing if it's less than, but it would be the subarray left of the middle
5. We repeat steps 2,3,4 for each smaller subarray section, until there is/isn't a match

The wiki article has some pretty good pictures to explain this process:
https://en.wikipedia.org/wiki/Binary_search_algorithm
