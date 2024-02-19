+++
title = 'Leetcode'
date = 2024-02-19T09:26:59+08:00
draft = false
+++

### 数组  
1. 最小操作次数使数组元素相等  
给你一个长度为 n 的整数数组，每次操作将会使 n - 1 个元素增加 1 。返回让数组所有元素相等的最小操作次数。
题解:  
```c
int minMoves(int* nums, int numsSize) {
    int temp = INT_MAX;
    for(int i = 0; i < numsSize; i++) {
        if(nums[i] < temp)
            temp = nums[i];
    }
    int ans = 0;
    for(int i = 0; i < numsSize; i++) {
        ans += nums[i] - temp;
    }
    return ans;    
}
```

2. 非递减数列  
给你一个长度为 n 的整数数组 nums ，请你判断在 最多 改变 1 个元素的情况下，该数组能否变成一个非递减数列。  
我们是这样定义一个非递减数列的： 对于数组中任意的 i (0 <= i <= n-2)，总满足 nums[i] <= nums[i + 1]。  
题解:  
```c
bool checkPossibility(int* nums, int numsSize) {
    int cnt = 0;
    for (int i = 0; i < numsSize - 1; ++i) {
        int x = nums[i], y = nums[i + 1];
        if (x > y) {
            cnt++;
            if (cnt > 1) {
                return false;
            }
            if (i > 0 && y < nums[i - 1]) {
                nums[i + 1] = x;
            }
        }
    }
    return true;
}
```
3. 移动零  
给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。  
请注意，必须在不复制数组的情况下原地对数组进行操作。  
题解:  
```c
void swap(int *a, int *b) {
    int t = *a;
    *a = *b, *b = t;
}

void moveZeroes(int *nums, int numsSize) {
    int left = 0, right = 0;
    while (right < numsSize) {
        if (nums[right]) {
            swap(nums + left, nums + right);
            left++;
        }
        right++;
    }
}
```
4. 轮转数组  
给定一个整数数组 nums，将数组中的元素向右轮转 k 个位置，其中 k 是非负数。  
示例:  
输入: nums = [1,2,3,4,5,6,7], k = 3  
输出: [5,6,7,1,2,3,4]
题解:  
方法一: 使用额外的数组  
```c
void rotate(int* nums, int numsSize, int k) {
    int newArr[numsSize];
    for (int i = 0; i < numsSize; ++i) {
        newArr[(i + k) % numsSize] = nums[i];
    }
    for (int i = 0; i < numsSize; ++i) {
        nums[i] = newArr[i];
    }
}
```
方法二: 数组翻转  
```c
void swap(int* a, int* b) {
    int t = *a;
    *a = *b, *b = t;
}

void reverse(int* nums, int start, int end) {
    while (start < end) {
        swap(&nums[start], &nums[end]);
        start += 1;
        end -= 1;
    }
}

void rotate(int* nums, int numsSize, int k) {
    k %= numsSize;
    reverse(nums, 0, numsSize - 1);
    reverse(nums, 0, k - 1);
    reverse(nums, k, numsSize - 1);
}
```
