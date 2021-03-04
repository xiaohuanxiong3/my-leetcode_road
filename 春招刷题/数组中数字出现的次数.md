在一个数组 nums 中除一个数字只出现一次之外，其他数字都出现了三次。请找出那个只出现一次的数字。

#### 示例一:
```
输入：nums = [3,4,3,3]
输出：4
```

#### 示例二:
```
输入：nums = [9,1,7,9,7,9,7]
输出：1
```

### 限制:
 * `1 <= nums.length <= 10000`
 * `1 <= nums[i] < 2^31`
---
解法1:使用HashMap计数

```bash
class Solution {
    private Map<Integer,Integer> map = new HashMap<Integer,Integer>(); 
    private int ans;
    public int singleNumber(int[] nums) {
        for(int i=0;i<nums.length;i++){ // 用map对数组元素计数
            map.put(nums[i],map.get(nums[i])==null ? 1 : map.get(nums[i])+1 );
        }
        // Iterator泛型
        Iterator<Map.Entry<Integer,Integer>> entries = map.entrySet().iterator();
        while(entries.hasNext()){
            Map.Entry<Integer,Integer> entry = entries.next();
            if(entry.getValue() == 1 )
            {
                ans = entry.getKey();
                break;
            }
        }
        return ans;
    }
}
````

解法2：两重循环+按位异或

```bash
class Solution {
    private int cnt,ans;
    public int singleNumber(int[] nums) {
        for(int i = 0;i<nums.length;i++){
            cnt = 0;
            for(int j = 0;j<nums.length ;j++ )
            {
                if( (nums[i] ^ nums[j]) == 0 ) // 值相同
                    cnt++;
            }
            if( cnt == 1 )
            {
                ans = nums[i];
                break;
            }
        }
        return ans;
    }
}
```
 
解法3: 考虑数字的二进制形式，对于出现三次的数字，各 二进制位 出现的次数都是 3 的倍数。
因此，统计所有数字的各二进制位中 1 的出现次数，并对 3 求余，结果则为只出现一次的数字。

#### 代码如下:
```
class Solution {
    public int singleNumber(int[] nums) {
        int[] counts = new int[32];
        for(int num : nums) {
            for(int i = 0; i < 32; i++) {
                counts[i] += num & 1; // 更新第 i 位 1 的个数之和
                num >>= 1;            // 第 i 位 --> 第 i 位
            }
        }
        int res = 0, m = 3;
        for(int i = 31; i >= 0; i--) {
            res <<= 1;
            res |= counts[i] % m;     // 恢复第 i 位
        }
        return res;
    }
}

```

详细解析如下:[第一种解法没懂](https://leetcode-cn.com/leetbook/read/illustration-of-algorithm/9hctss/)
