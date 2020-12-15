# DATA STRUCTURES AND ALGORITHMS

## Questions Curated by : take U forward (Youtube Channel)
## [Link to Questions](https://docs.google.com/document/d/1SM92efk8oDl8nyVw8NHPnbGexTS9W-1gmTEYfEurLWQ/edit)

### Note : I am not following best coding practices like adding descriptive names to variables, commenting codes etc. as I want to solve as many questions as possible to understand how to apply basic data structures and algorithms to coding questions

## Table of Content
 
| Topic               |
|---------------------|        
| Array               |
| Maths               |
| Hashing             |
| LinkedList          |
| 2-Pointer           |
| Greedy              |
| Backtracking        |
| Divide and Conquer  |
| Bits                |
| Stack and Queue     |
| Strings             |
| Binary Tree         |
| Binary Search Tree  |
| Mixed Questions     |
| Graph               |
| Dynamic Programming |

<br/>

## Arrays

### Question 1 : Find the Duplicate Number
### [Link to Question](https://leetcode.com/problems/find-the-duplicate-number/)

### **CODE**
```c++
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        if(nums.size() <= 1) return -1;
        int slow = 0, fast = 0, n = nums.size();
        slow = nums[slow];
        fast = nums[nums[fast]];
        while(slow != fast) {
            slow = nums[slow];
            fast = nums[nums[fast]];
        }
        slow = 0;
        while(slow != fast) {
            slow = nums[slow];
            fast = nums[fast];
        }
        return slow;
    }
// First the slow pointer goes 1 step and fast pointer goes 2 steps 
// at a time and then both the pointers goes 1 step at a time
};
```

#### Time Complexity : O(n), where n is the size of the array
#### Space Complexity : O(1)

<br/>


### Question 2 : Sort Colors
### [Link to Question](https://leetcode.com/problems/sort-colors/)

### **CODE**
```c++
class Solution {
public:
    void sortColors(vector<int>& nums) {
        if(nums.size() == 0 || nums.size() == 1) return;
        int n = nums.size();
        int start = 0, pointer = 0, end = n-1;
        while(start < end && pointer <= end) {
            if(nums[pointer] == 0) {
                swap(nums[start],nums[pointer]);
                start++;
                pointer++;
            }
            else if(nums[pointer] == 2) {
                swap(nums[pointer], nums[end]);
                end--;
            }
            else
                pointer++;
        }
    }
};
```

#### Time Complexity: O(n), where n is the size of the array
#### Space Complexity: O(1)

<br/>


### Question 3 : Merge Sorted Array
### [Link To Question](https://leetcode.com/problems/merge-sorted-array/)

### **CODE**
```c++
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int start = 0, mid = m, i = 0;
        while(i < n) {
            if(start == mid) {
                for(int j = i; j < n; j++) {
                    nums1[start] = nums2[j];
                    start++;
                }
                break;
            }
            if(nums1[start] >= nums2[i]) {
                for(int j = mid; j > start; j--) {
                    nums1[j] = nums1[j-1];
                }
                nums1[start] = nums2[i];
                start++;
                i++;
                mid++;
            }
            else
                start++;
        }
    }
};
```

#### Time Complexity: O(n+m)
#### Space Complexity: O(1)

<br>


### Question 4 : Maximum Subarray Sum
### [Link to Question](https://leetcode.com/problems/maximum-subarray/)

### **CODE**
```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        long long curr_sum = -1e18, max_sum = -1e18;
        for(int i = 0; i < nums.size(); i++) {
            curr_sum = max(1LL*nums[i], 1LL*nums[i]+curr_sum);
            max_sum = max(curr_sum, max_sum);
        }
        return (int)max_sum;
    }
};
```

#### Time Complexity : O(n), where n is the size of the array
#### Space Complexity : O(1)

<br>


### Question 5 : Merge Intervals
### [Link to Question](https://leetcode.com/problems/merge-intervals/)

### **CODE**
```c++
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        if(intervals.size() < 2)
            return intervals;
        sort(intervals.begin(), intervals.end());
        vector<vector<int>> a;
        int mx = intervals[0][1];
        for(int i = 1; i < intervals.size(); i++) {
            if(intervals[i][0] <= mx) {
                if(!a.empty()) {
                    if(a[a.size()-1][1] >= intervals[i][0]) {
                        a[a.size()-1][1] = max(intervals[i][1], a[a.size()-1][1]);
                        mx = max(intervals[i][1], a[a.size()-1][1]);
                    }
                }
                else {
                    vector<int> temp;
                    temp.push_back(intervals[i-1][0]);
                    temp.push_back(max(intervals[i][1], intervals[i-1][1]));
                    a.push_back(temp);
                    mx = max(intervals[i][1], intervals[i-1][1]);
                }
            }
            else {
                if(!a.empty()) {
                    a.push_back(intervals[i]);
                    mx = max(mx, intervals[i][1]);
                }
                else {
                    a.push_back(intervals[i-1]);
                    a.push_back(intervals[i]);
                    mx = max(mx, intervals[i][1]);
                }
            }
        }
        return a;
    }
};
```

#### Time Complexity : O(nlogn), where n is the size of intervals array
#### Space Complexity : O(1)