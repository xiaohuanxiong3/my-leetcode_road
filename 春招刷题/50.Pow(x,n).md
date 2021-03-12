实现 pow(x, n) ，即计算 x 的 n 次幂函数（即，xn）。

#### 示例 1：
```
输入：x = 2.00000, n = 10
输出：1024.00000
```

#### 示例 2：
```
输入：x = 2.10000, n = 3
输出：9.26100
```

#### 示例 3：
```
输入：x = 2.00000, n = -2
输出：0.25000
解释：2-2 = 1/22 = 1/4 = 0.25
```

#### 提示：
* -100.0 < x < 100.0
* -231 <= n <= 231-1
* -104 <= xn <= 104

#### [使用快速幂算法,注意临界条件](https://leetcode-cn.com/leetbook/read/programmation-efficace/9bh5eh/)
```
class Solution {
    public double myPow(double x, int n) {
        int p2 = 1; 
        double xp2 = x;
        double result = 1.0;
        boolean flag = false;
        boolean md = false;
        if( n<0 ){ // n为负数即为求倒数
            if( n == -2147483648 ){
                n += 2; // -2147483648求相反数会超过INT型的取值范围,加2是为了不影响结果的正负
                md = false;
            }; 
            n = -n;
            flag = true;
        } 
        while( n>0 ){
            if( (n & p2) > 0){ // n可由p2相加得来
                n -= p2;
                result *= xp2;
            }
            p2 = p2<<1;
            xp2 = xp2 * xp2;
        }
        if( md ) result = result * x * x; // 少乘了一次得加上
        if( flag ) result = 1/result;
        return result;
    }
}
```
