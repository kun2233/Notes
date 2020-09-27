# <span style='color:#f37b1d'>鲲小白刷Leetcode题笔记</span>

### <span style='color:blue'>**题目1 两数之和**</span>

```
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。
```

示例:
给定 

```
nums = [2, 7, 11, 15], target = 9
```

因为 

```
nums[0] + nums[1] = 2 + 7 = 9
```

所以返回 

```
[0, 1]
```

**解法一（暴力破解）：**

```java
class Solution {  
    public int[] twoSum(int[] nums, int target) {    
        int[] a= new int[2];    
        for(int i = 0; i < nums.length; i++){      
            for(int j = i+1; j<nums.length;j++){        
                if(nums[i]+nums[j]==target){          
                    a[0]=i;          
                    a[1]=j;          
                    return a;        
                }      
            }    
        }  
        throw new IllegalArgumentException("No two sum solution");  
    }
}
```

**时间复杂度：**O(n^2)
对于每个元素，会试图通过遍历数组的其余部分来寻找它所对应的目标元素，这将耗费 O(n)的时间。因此时间复杂度为 O(n^2)。
**空间复杂度**：O(1)。

**解法二(哈希表）：java**

哈希表数组链表数据结构，下标存的是原数组的值，内存里存的是下标。

由于哈希查找的时间复杂度为 O(1)，所以可以利用哈希容器 map 降低时间复杂度
遍历数组 nums，i 为当前下标，每个值都判断map中是否存在 target-nums[i] 的 key 值
如果存在则找到了两个值，如果不存在则将当前的 (nums[i],i) 存入 map 中，继续遍历直到找到为止



```java
class Solution{  
    public int[] twoSum(int[] nums, int target){    
        Map<Integer,Integer> map = new HashMap<>();     
        for(int i=0; i<nums.length;i++){      
            int complement = target - nums[i];      
            if(map.containsKey(complement)){        
                return new int[] {map.get(complement),i};      
            }      
            map.put(nums[i],i);    
        }  
    }
}
```

**时间复杂度：**O(n)

只遍历了包含有 n*n* 个元素的列表一次。在表中进行的每次查找只花费 O(1)*O*(1) 的时间

**空间复杂度**：O(n)

所需的额外空间取决于哈希表中存储的元素数量，该表最多需要存储 n*n* 个元素。