# Day 1: Array Manipulation Fundamentals

Let's break down the key array manipulation techniques that frequently appear in coding assessments, with examples and implementation approaches.

## Two-Pointer Technique

This technique uses two pointers to solve problems with sorted arrays or when searching for pairs with specific properties.

### Example Problem: Two Sum in Sorted Array

**Problem**: Given a sorted array of integers and a target value, find two numbers that add up to the target.

**Solution**:
```python
def two_sum_sorted(nums, target):
    left, right = 0, len(nums) - 1
    
    while left < right:
        current_sum = nums[left] + nums[right]
        
        if current_sum == target:
            return [left, right]  # or return [nums[left], nums[right]]
        elif current_sum < target:
            left += 1  # Need a larger sum, move left pointer right
        else:
            right -= 1  # Need a smaller sum, move right pointer left
            
    return []  # No solution found
```
**My interpretation**:
This is easy... 
if smaller than target, go 1 to the right
if larger than target, go 1 to the left
Until the sum matched the target, return
if nothing == target is found even when left meets right, return []
and use left < right is because we don't want them to meet (dont use same elem twice)


### Example Problem: Remove Duplicates from Sorted Array

**Problem**: Remove duplicates from a sorted array in-place and return the new length.

**Solution**:
```python
def remove_duplicates(nums):
    if not nums:
        return 0
        
    # Position to place the next unique element
    insert_pos = 1
    
    for i in range(1, len(nums)):
        # If current element is different from the previous one
        if nums[i] != nums[i-1]:
            nums[insert_pos] = nums[i]
            insert_pos += 1
            
    return insert_pos  # New length
```
**My interpretation**:
Not an easy question at first glance, because of the `insert_pos = 1` stuff
if the current elem is the same as prev elem:
--> don't increment `insert_pos`, 
--> so when next 'different elem' happens, that 'different elem' is copied to the `insert_pos`. 
--> which is the first repeting index (because it doesn't change since then, it doesn't enter the if loop)

You've got a good understanding of the mechanics, but let me help clarify the approach for tackling this problem from first principles.

**Claude Suggestions**
When you encounter a problem like this (removing duplicates in-place), here's how to approach it:

1. **Recognize the pattern**: We need a way to overwrite duplicates while preserving unique elements in their original order.

2. **Two-pointer strategy**: One pointer (`i`) scans through the array, and another pointer (`insert_pos`) keeps track of where to place the next unique element.

3. **Mental model**: Think of it as "building a new array in-place" where `insert_pos` represents the end of our result array so far.

Interesting, removing (in place) = building an array, I like this approach.

but if the array is not sorted... you cant do that right cuz the replicate could happen outside of consective elem



You're absolutely right. For unsorted arrays, this specific consecutive element comparison approach wouldn't work.

If the array isn't sorted, duplicates could be scattered throughout the array rather than appearing consecutively. In that case, you'd need a different strategy:

**Using a hash set/table**: Keep track of elements you've already seen
   ```python
   def remove_duplicates_unsorted(nums):
       if not nums:
           return 0
           
       seen = set()
       insert_pos = 0
       
       for i in range(len(nums)):
           if nums[i] not in seen:
               seen.add(nums[i])
               nums[insert_pos] = nums[i]
               insert_pos += 1
               
       return insert_pos
   ```



## Merging Sorted Arrays

**Problem**: Merge two sorted arrays into a single sorted array.

**Solution**:
```python
def merge_sorted_arrays(nums1, nums2):
    result = []
    i, j = 0, 0
    
    # Compare elements from both arrays and add the smaller one
    while i < len(nums1) and j < len(nums2):
        if nums1[i] <= nums2[j]:
            result.append(nums1[i])
            i += 1
        else:
            result.append(nums2[j])
            j += 1
    
    # Add remaining elements
    result.extend(nums1[i:])
    result.extend(nums2[j:])
    
    return result
```

**My interpretation**:
always append the smaller one after comparision,
then also don't forget to increment the index of the smaller one side


**Claude**
1. Always select the smaller element from the two arrays to maintain sorted order
2. Remember to increment only the pointer for the array from which you took the element
3. After one array is exhausted, append all remaining elements from the other array


## Practice Problems

Here are three problems to practice these concepts:

1. **Three Sum**: Find all unique triplets in an array that sum to zero.
   - Sort the array first
   - For each element, use two-pointer technique to find pairs that sum to its negative

2. **Container With Most Water**: Given heights of walls, find the maximum water container.
   - Use two pointers at both ends
   - Move the pointer with the smaller height inward

3. **Sort Colors** (Dutch National Flag problem): Sort an array with only three distinct values.
   - Use three pointers to track positions of 0s, 1s and 2s

## Key Concepts to Remember:

1. When dealing with sorted arrays, the two-pointer technique often provides O(n) solutions
2. For unsorted arrays, consider sorting first (O(n log n)) if it simplifies the solution
3. In-place array manipulation often uses a "fast" and "slow" pointer approach
4. Many array problems can be solved by traversing once with careful pointer management

Would you like me to provide a more detailed walkthrough of any of these problems, or shall we move on to Day 2's concept?