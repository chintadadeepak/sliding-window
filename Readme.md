# Sliding Window Source Codes

## Different Patterns under Sliding Window.

1. Constant Window
2. Longest Subarray Array or Substring
3. Count subarrays with condition
4. Minimum / Smallest window

## Naive Solution for constant window

```cpp
int largestSum(vector<int> &nums, int k) {
    int size = nums.size();
    int result = INT_MIN;
    for(int i = 0; i < size - k + 1; i++) {
        int localSum = 0;
        for(int j = i; j < k + i; j++)
            localSum += nums[j];
        if(localSum > sum)
            result = localSum;
    }
    return result;
}

TC: O(n*n)
SC: O(1)
```

## Two Pointer Solution for constant window

```cpp
int largestSum(vector<int> &nums, int k) {
    int size = nums.size();
    int result = INT_MIN;
    int left = right = 0;
    int sum = 0;
    for(right = 0; right < k; right++)
        sum += nums[right];
    result = max(result, sum);
    while(right < size) {
        sum -= nums[left++];
        sum += nums[right++];
        result = max(result, sum);
    }
    return result;
}

TC: O(2*n)
SC: O(1)
```

## Naive Solution for Longest Subarray with condition

```cpp
int longestSubarray(vector<int> &nums, int k) {
    int size = nums.size();
    int result = INT_MIN;
    for(int i = 0; i < size; i++) {
        int sum = 0;
        for(int j = i; j < size; j++) {
            sum += nums[j];
            if(sum <= k)
                result = max(result, j - i + 1);
            else
                // this condition is not valid, if array -ve numbers
                break;
        }
    }
    return result;
}

TC: O(n*n)
SC: O(1)
```

## Better Solution for Longest Subarray with condition

```cpp
int longestSubarray(vector<int> &nums, int k) {
    int size = nums.size();
    int result = INT_MIN;
    int left = right = 0;
    int sum = 0;
    while(right < size) {
        sum += nums[right];
        while(sum > k)
            sum -= nums[left++];
        result = max(result, right - left + 1);
        right++;
    }
    return result;
}

TC: O(2*n)
SC: O(1)
```

## Optimal Solution for Longest Subarray with condition

```cpp
int longestSubarray(vector<int> &nums, int k) {
    int size = nums.size();
    int result = INT_MIN;
    int left = right = 0;
    int sum = 0;
    while(right < size) {
        sum += nums[right];
        if(sum > k)
            sum -= nums[left++];
        result = max(result, right - left + 1);
        right++;
    }
    return result;
}

TC: O(n)
SC: O(1)
```
