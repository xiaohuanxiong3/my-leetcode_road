在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。

#### 示例1:
```
输入: [7,5,6,4]
输出: 5
```

#### 限制:
`0 <= 数组长度 <= 50000`

#### 解法一：利用递归排序
```
class Solution {
    private int[] temp = new int[50000];
    private int ans = 0;
    public int reversePairs(int[] nums) {
        Merge_sort(nums,0,nums.length);
        return ans;
    }
    // 对nums数组的l->r-1进行归并排序
    public void Merge_sort(int[] nums,int l,int r){
        if( l>=r-1 ) return;
        int mid = (r+l)/2;
        Merge_sort(nums,l,mid); // l->mid-1
        Merge_sort(nums,mid,r); // mid->r-1
        Merge(nums,l,mid,r);
    }
    public void Merge(int[] nums,int l,int mid,int r){
        int p=l,q=mid,s=l;
        while(p<mid && q<r){
            if( nums[p]>nums[q] ){
                temp[s++] = nums[q++];
                ans += mid-p;
            }
            else temp[s++] = nums[p++];
        }
        while(p<mid) temp[s++] = nums[p++];
        while(q<r) temp[s++] = nums[q++];
        for(int i=l;i<r;i++){
            nums[i] = temp[i];
        }
    }
}
```
