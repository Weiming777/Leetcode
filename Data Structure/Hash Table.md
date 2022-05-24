# **Two Sum**

**Example 1:**

```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

**Example 2:**

```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

**Example 3:**

```java
Input: nums = [3,3], target = 6
Output: [0,1]
```



### Solution 1：Brute Force

Time complexity: O(n^2). 

```java
class Solution{
		public int[] twoSum(int[] nums, int target) {
			for (int i = 0; i < nums.length; i++){
				for(int j = i + 1; j < nums.length; j++){
        	if (nums[i] + nums[j] == target){
            return new int[] {i,j}; 
          }
        }
			}
      return null;
		}
}
```

```java
new int[] {}   // initialize
```



### Solution 2: HashMap

Time complexity: O(n).

```java
class Solution{
		public int[] twoSum(int[] nums, int target) {
      Map<Integer, Integer> map = new HashMap<>();
      for (int i = 0; i < nums.length ; i++){
        int temp = target - nums[i];
        if (map.containsKey(temp)){
          return new int[] {i , map.get(temp)};
        }
        map.put(nums[i] , i);
      }
      return null;
    }
}
```

