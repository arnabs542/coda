### 442. Find All Duplicates in an Array ****
Given an array of integers, 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements that appear twice in this array.

Could you do it without extra space and in O(n) runtime?
```
Example:
Input:
[4,3,2,7,8,2,3,1]

Output:
[2,3]
```
```java
/*
alg: swap each nums[i] to position i - 1, continue until the element in in position or we find a duplicate
    - when find a duplicate, to avoid finding it again, we set the duplicate to -1, special placeholder

time: O(n)
space: O(1)
*/
class Solution {
    public List<Integer> findDuplicates(int[] nums) {
        List<Integer> res = new ArrayList<>();
        if (nums == null || nums.length == 0) {
            return res;
        }
        /*
        index map:
            for each nums[i], its corresp location index = nums[i] - 1
        */
        for (int i = 0; i < nums.length; i++) {
            while (nums[i] != -1 && nums[i] - 1 != i) {
                //check if duplicate
                if (nums[i] == nums[nums[i] - 1]) {
                    res.add(nums[i]);
                    nums[i] = -1;
                } else {
                    swap(nums, i, nums[i] - 1);
                }
            }
        }
        return res;
    }
    public void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```