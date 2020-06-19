# CRACKING  THE CODING INTERVIEW

## Solving 159 questions in 26 days
## Questions Curated by : take U forward (Youtube Channel)
## [Link to Questions](https://docs.google.com/document/d/1SM92efk8oDl8nyVw8NHPnbGexTS9W-1gmTEYfEurLWQ/edit)

## Table of Content
 
| Days       | Topic               |
|------------|---------------------|        
| Day 1      | Array               |
| Day 2      | Array               |
| Day 3      | Maths               |
| Day 4      | Hashing             |
| Day 5      | LinkedList          |
| Day 6      | LinkedList          |
| Day 7      | 2-Pointer           |
| Day 8      | Greedy              |
| Day 9      | Backtracking        |
| Day 10     | Backtracking        |
| Day 11     | Divide and Conquer  |
| Day 12     | Bits                |
| Day 13     | Stack and Queue     |
| Day 14     | Stack and Queue     |
| Day 15     | Strings             |
| Day 16     | Strings             |
| Day 17     | Binary Tree         |
| Day 18     | Binary Tree         |
| Day 19     | Binary Tree         |
| Day 20     | Binary Search Tree  |
| Day 21     | Binary Search Tree  |
| Day 22     | Mixed Questions     |
| Day 23     | Graph               |
| Day 24     | Graph               |
| Day 25     | Dynamic Programming |
| Day 26     | Dynamic Programming |

<br/>

## Day 1 : Arrays

### Question 1 : Find All Duplicates in an Array
### [Link to Question](https://leetcode.com/problems/find-all-duplicates-in-an-array/)

### Solution : 
> #### We need to solve this question in O(n) time and O(1) space. We know that 1 <= a[i] <= n, so we can use the indexes to check whether an element exists twice. For every element a[i] mark it's index a[a[i]-1] as negative. Now if a[a[i]-1] is already negative for any element that means it is already visited and we can insert the element in a list.
### **CODE**
```c++
class Solution {
public:
    vector<int> findDuplicates(vector<int>& nums) {
        vector<int> duplicates;
        for(int i = 0; i < nums.size(); i++) {
            if(nums[abs(nums[i])-1] < 0)
                duplicates.push_back(abs(nums[i]));
            else
                nums[abs(nums[i])-1] = -nums[abs(nums[i])-1];
        }
        return duplicates;
    }
};
```
<br/>

### Question 3 : Find the repeating and the missing
### [Link to Question](https://www.hackerrank.com/contests/kcertc/challenges/find-the-repeating-and-the-missing/problem)

### Solution :
> #### First we will use a hash table to keep track of the frequency of each element. This will help us find out which element appears twice. Next, we will calculate the sum of all the elements in the array and subtract the duplicate number from it. We will also calculate the actual sum of the array using the formula n*(n+1)/2. The difference of actual sum and sum of the array will give us the missing number. 

### **CODE**
```c++
#include <bits/stdc++.h>
using namespace std;

int main() { 
    int n;
    cin >> n;
    vector<int> arr(n);
    for(int i = 0; i < n; i++)
        cin >> arr[i];
    unordered_map<int, int> frequency;
    int missing_num;
    for(auto x: arr) {
        if(frequency[x] == 1) {
            missing_num = x;
            break;
        }
        else 
            frequency[x]++;
    }
    long long int sum = 0, actual_sum = 0;
    for(auto x: arr)
        sum += x;
    actual_sum = (arr.size()*(arr.size()+1))/2;
    sum -= missing_num;
    cout << actual_sum-sum << "," << missing_num << "\n";
    
    return 0;
}
```
<br/>



