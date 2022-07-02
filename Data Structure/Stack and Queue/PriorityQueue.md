# 347.Top K Frequent Elements

Given an integer array `nums` and an integer `k`, return *the* `k` *most frequent elements*. You may return the answer in **any order**.

 

**Example 1:**

```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

**Example 2:**

```
Input: nums = [1], k = 1
Output: [1]
```







## Solution : PriorityQueue

```java
  	//(n1, n2) -> map.get(n1) - map.get(n2)  or  （o1,o2) -> o1.getValue() - o2.getValue()  小顶堆  MinHeap
  	//(n1, n2) -> map.get(n2) - map.get(n1)  or  （o1,o2) -> o2.getValue() - o1.getValue()  大顶堆  MaxHeap
```

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        
        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        
        Queue<Integer> heap = new PriorityQueue<>((n1, n2) -> map.get(n1) - map.get(n2));
      	//(n1, n2) -> map.get(n1) - map.get(n2)  or  （o1,o2) -> o1.getValue() - o2.getValue()  小顶堆
      	//(n1, n2) -> map.get(n2) - map.get(n1)  or  （o1,o2) -> o2.getValue() - o1.getValue()  大顶堆
        
        for (int n: map.keySet()) {
          heap.add(n);
          if (heap.size() > k) heap.poll();    
        }
        
        int[] top = new int[k];
        for(int i = k - 1; i >= 0; --i) {
            top[i] = heap.poll();
        }
        return top;
    }
}
```





## Solution :

求出数组中出现频率最高的k个数即可。思路也很清晰，首先可以遍历出数组中所有数及其出现次数并将其保存在HashMap中。然后将map转化为以出现次数为索引，数为值的数组。最后再反向遍历出出现次数最大的k个数即可.

```java
public List<Integer> topKFrequent(int[] nums, int k) {

	List<Integer>[] bucket = new List[nums.length + 1];
	Map<Integer, Integer> frequencyMap = new HashMap<Integer, Integer>();

	for (int n : nums) {
		frequencyMap.put(n, frequencyMap.getOrDefault(n, 0) + 1);
	}

	for (int key : frequencyMap.keySet()) {
		int frequency = frequencyMap.get(key);
		if (bucket[frequency] == null) {
			bucket[frequency] = new ArrayList<>();
		}
		bucket[frequency].add(key);
	}

	List<Integer> res = new ArrayList<>();

	for (int pos = bucket.length - 1; pos >= 0 && res.size() < k; pos--) {
		if (bucket[pos] != null) {
			res.addAll(bucket[pos]);
		}
	}
	return res;
}
```

