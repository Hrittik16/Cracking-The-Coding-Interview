# CRACKING  THE CODING INTERVIEW

## Solving 160 questions in 52 days (~ 2 months)
## Questions Curated by : take U forward (Youtube Channel)
## [Link to Questions](https://docs.google.com/document/d/1SM92efk8oDl8nyVw8NHPnbGexTS9W-1gmTEYfEurLWQ/edit)

## Table of Content
 
| Days           | Topic               |
|----------------|---------------------|        
| Day 1 - Day 4  | Array               |
| Day 5 - Day 6  | Maths               |
| Day 7 - Day 8  | Hashing             |
| Day 9 - Day 12 | LinkedList          |
| Day 13- Day 14 | 2-Pointer           |
| Day 15- Day 16 | Greedy              |
| Day 17- Day 20 | Backtracking        |
| Day 21- Day 22 | Divide and Conquer  |
| Day 23- Day 24 | Bits                |
| Day 25- Day 28 | Stack and Queue     |
| Day 29- Day 32 | Strings             |
| Day 33- Day 38 | Binary Tree         |
| Day 39- Day 42 | Binary Search Tree  |
| Day 43- Day 44 | Mixed Questions     |
| Day 45- Day 48 | Graph               |
| Day 49- Day 52 | Dynamic Programming |

<br/>

## Day 1 : Arrays

### Question 1 : Find All Duplicates in an Array
### [Link to Question](https://leetcode.com/problems/find-all-duplicates-in-an-array/)

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

### Question 2 : Find the repeating and the missing
### [Link to Question](https://www.hackerrank.com/contests/kcertc/challenges/find-the-repeating-and-the-missing/problem)

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

### Question 3 : Maximum Subarray
### [Link to Question](https://leetcode.com/problems/maximum-subarray/)

### **CODE**
```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        long long int curr_sum = -1e18, best_sum = -1e18;
        for(int i = 0; i < nums.size(); i++) {
            curr_sum = max((long long int)nums[i], (long long int)curr_sum+nums[i]);
            best_sum = max(best_sum, curr_sum);
        }
        return best_sum;
    }
};
```
<br/>

## Day 2 : Arrays

### Question 4 : Sort Colors
### [Link to Question](https://leetcode.com/problems/sort-colors/)

### **CODE**
```c++
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int n = nums.size();
        int beg = 0, end = n-1, mid = 0;
        while(mid <= end) {
            if(nums[mid] != 0 && nums[mid] != 2)
                mid++;
            else if(nums[mid] == 0) {
                swap(nums[beg], nums[mid]);
                beg++;
                mid++;
            }
            else if(nums[mid] == 2) {
                swap(nums[end], nums[mid]);
                end--;
            }
        }
    }
};
```
<b2/>

### Question 5 : Merge Sorted Array
### [Link to Question](https://leetcode.com/problems/merge-sorted-array/)

### **CODE**
```c++
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int i = m-1, j = n-1, k = m+n-1;
        while(i >= 0 && j >= 0) {
            if(nums1[i] > nums2[j]) {
                nums1[k] = nums1[i];
                k--;
                i--;
            }
            else {
                nums1[k] = nums2[j];
                k--;
                j--;
            }
        }
        while(j >= 0) {
            nums1[k] = nums2[j];
            k--;
            j--;
        }
    }
};
```
<br/>

### Question 6 : Merge Intervals
### [Link to Question](https://leetcode.com/problems/merge-intervals/)

### **CODE**
```c++
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        if(intervals.size() == 0) {
            vector<vector<int>> result;
            return result;
        }
        sort(intervals.begin(), intervals.end());
        vector<vector<int>> result;
        result.push_back(intervals[0]);
        for(int i = 1; i < intervals.size(); i++) {
            if(result.back().back() < intervals[i].front())
                result.push_back(intervals[i]);
            else 
                result.back().back() = max(result.back().back(), intervals[i].back());
        }
        return result;
    }
};
```

## Day 3: Arrays

### Question 7 : Set Matrix Zeroes
### [Link to Question](https://leetcode.com/problems/set-matrix-zeroes/)

### **CODE**
```c++
class Solution {
public:
    
    void print_matrix(vector<vector<int>>& matrix) {
        for(int i = 0; i < matrix.size(); i++) {
            for(int j = 0; j < matrix[0].size(); j++)
                cout << matrix[i][j]  << " ";
            cout << "\n";
        }
    }
    
    void setZeroes(vector<vector<int>>& matrix) {
        // Find the last row containing 0
        // Go through all the rows till last row and mark the equivalent column in last row as 0
        // Go through 1st row all the columns and if the equivalent column in last row containing 0
        // is 0, then make the entire column 0
        
        int m = matrix.size(), n = matrix[0].size();
        int last = -1;
        for(int i = m-1; i >= 0 && last == -1; i--) {
            for(int j = 0; j < n; j++) {
                if(matrix[i][j] == 0) {
                    last = i;
                    break;
                }
            }
        }
        if(last == -1)
            return;
        for(int i = 0; i < last; i++) {
            bool zero = false;
            for(int j = 0; j < n; j++) {
                if(matrix[i][j] == 0) {
                    matrix[last][j] = 0;
                    zero = true;
                }
            }
            if(zero) {
                for(int k = 0; k < n; k++)
                    matrix[i][k] = 0;
            }
        }
        
        //print_matrix(matrix);
        
        for(int j = 0; j < n; j++) {
            if(matrix[last][j] == 0) {
                for(int i = 0; i < m; i++) {
                    matrix[i][j] = 0;
                }
            }
        }
        
        for(int j = 0; j < n; j++)
            matrix[last][j] = 0;
        
    }
};
```