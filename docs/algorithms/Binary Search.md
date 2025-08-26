I know binary search feels like a trivial algorithm, but I guess if I had to say which algo I struggled with the most despite knowing the concept, it'd be the *Binary Search*. The concept is clear, but I always make mistakes with where to put `<=` or `<`. So, here's a standard template that should work for finding a target value in a sorted array.

# Typical Binary Search

There are a few key points to focus on when writing a binary search algorithm. I'll provide reasons for each, but memorizing them works as well.

1.  **Main `while` loop condition**: Keep it `while left <= right`.
    -   This ensures that the search continues as long as there is at least one element in the search space. When `left` becomes greater than `right`, it means the search space is empty.

2.  **Modifying `left` and `right`**: Always update `left` or `right` by **1** to shrink the search space.
    -   If `arr[mid] < target`, the target must be in the right half, so we set `left = mid + 1`.
    -   If `arr[mid] > target`, the target must be in the left half, so we set `right = mid - 1`.

3.  **Early Exit**: We can stop early if we find the target.
    -   If `arr[mid] == target`, we've found the element and can return `mid` immediately.

4.  **Return Value**:
    -   If the target is found, we return its index.
    -   If the loop finishes without finding the target.
        - After the loop finished the inequality relation will be `right < target < left`, i.e. right will point to largest element smaller than target and left will point to smallest element larger than the target.
        - Depending on the use case we might want to return. For example, we would return `left` for insert position.

```python
def binary_search(arr, target):
    left = 0
    right = len(arr) - 1

    while left <= right:
        mid = left + (right - left) // 2  # (1)!

        if arr[mid] == target:
            return mid  # (2)!
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return right  # (3)!
```

1.  This way of calculating the middle index helps in avoiding integer overflow in languages with fixed-size integers.
2.  Found the target, return its index
3.  Target not found, will need to return left or right depending on the use case.

