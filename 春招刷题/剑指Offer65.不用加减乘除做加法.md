写一个函数，求两个整数之和，要求在函数体内不得使用 “+”、“-”、“*”、“/” 四则运算符号。

#### 示例:
```
输入: a = 1, b = 1
输出: 2
```

#### 注意:
* a, b 均可能是负数或 0
* 结果不会溢出 32 位整数

代码如下:([虽然误打误撞之下做出来了，但是负数加法原理还是没搞懂](https://leetcode-cn.com/leetbook/read/illustration-of-algorithm/5vs8w7/))
```
class Solution {
    public int add(int a, int b) {
        int jinwe = (a&b)<<1;
        int ans = a ^ b;
        while( jinwe !=0 ){
            int temp = (ans & jinwe) << 1; // 更新后的进位
            ans = ans ^ jinwe; // 求和
            jinwe = temp;
        }
        return ans;
    }
}
```
