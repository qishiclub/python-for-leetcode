# Templates

## Sliding Window Pattern

```python
def sliding_window(nums: list[int], k: int) -> int:
    """
    Find max sum of any subarray of size k in nums.
    """
    n = len(nums)
    if n < k:
        return 0

    window_sum = sum(nums[:k])
    max_sum = window_sum
    for i in range(n - k):
        window_sum = window_sum - nums[i] + nums[i + k]
        max_sum = max(max_sum, window_sum)
    return max_sum
```

## Two Pointers Pattern

```python
def two_pointers(nums: list[int], target: int) -> tuple[int, int]:
    """
    find indices of two numers in sorted array to find the target sum.
    """
    left, right = 0, len(nums) - 1
    while left < right:
        current_sum = nums[left] + nums[right]
        if current_sum == target:
            return (left, right)
        elif current_sum < target:
            left += 1
        else:
            right -= 1
    return None
```

## Fast and Slow Pointers Pattern

```python
class ListNode:
    def __init__(self, value=0, next=None):
        self.value = value
        self.next = next

def has_cycle(head: ListNode) -> bool:
    """
    Detect if a linked list has a cycle.
    """
    slow = head
    fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    return False
```

## Merge Intervals Pattern

```python
def merge_intervals(intervals: list[tuple[int, int]]) -> list[tuple[int, int]]:
    """
    Merge overlapping intervals.
    """
    if not intervals:
        return []

    intervals.sort(key=lambda x: x[0])
    merged = [intervals[0]]

    for start, end in intervals[1:]:
        last_start, last_end = merged[-1]
        if start <= last_end:
            merged[-1] = (last_start, max(last_end, end))
        else:
            merged.append((start, end))
    return merged
```
