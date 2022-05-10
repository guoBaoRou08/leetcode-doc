**每日一题**

#### [908. 最小差值 I](https://leetcode-cn.com/problems/smallest-range-i/)

难度简单162收藏分享切换为英文接收动态反馈

给你一个整数数组 `nums`，和一个整数 `k` 。

在一个操作中，您可以选择 `0 <= i < nums.length` 的任何索引 `i` 。将 `nums[i]` 改为 `nums[i] + x` ，其中 `x` 是一个范围为 `[-k, k]` 的整数。对于每个索引 `i` ，最多 **只能** 应用 **一次** 此操作。

`nums` 的 **分数** 是 `nums` 中最大和最小元素的差值。 

*在对 `nums` 中的每个索引最多应用一次上述操作后，返回 `nums` 的最低 **分数*** 。

 

**示例 1：**

```
输入：nums = [1], k = 0
输出：0
解释：分数是 max(nums) - min(nums) = 1 - 1 = 0。
```

**示例 2：**

```
输入：nums = [0,10], k = 2
输出：6
解释：将 nums 改为 [2,8]。分数是 max(nums) - min(nums) = 8 - 2 = 6。
```

**示例 3：**

```
输入：nums = [1,3,6], k = 3
输出：0
解释：将 nums 改为 [4,4,4]。分数是 max(nums) - min(nums) = 4 - 4 = 0。
```

 

**提示：**

- `1 <= nums.length <= 104`

- `0 <= nums[i] <= 104`

- `0 <= k <= 104`

  

**题干截图**
![输入图片说明](%E5%9B%BE%E7%89%87/%E6%AF%8F%E6%97%A5%E4%B8%80%E9%A2%98.png)


**代码分析**



思路与算法

详细见代码注释。

主要数学运算求解



**代码截图**

![输入图片说明](%E5%9B%BE%E7%89%87/%E4%BB%A3%E7%A0%81%E6%88%AA%E5%9B%BE.png)

**解题源码**

`

```


package leetcode.editor.cn;

import java.util.Arrays;

//Java：最小差值 I


 class P908SmallestRangeI{
    public static void main(String[] args) {
        Solution solution = new P908SmallestRangeI().new Solution();
        // TO TEST
        int [] nums = {0,-10,-5,-10,-6,-9};
        int res = solution.smallestRangeI(nums,0);
        System.out.println("输入："+Arrays.toString(nums));
        System.out.println("输出："+res);
    }
    //leetcode submit region begin(Prohibit modification and deletion)

        class Solution {

            public int smallestRangeI(int[] nums, int k) {
                //分别从数组中获得最大值和最小值
                int minNum = Arrays.stream(nums).min().getAsInt();
                int maxNum = Arrays.stream(nums).max().getAsInt();
                //由题目可得nums 的 分数 是 nums 中最大和最小元素的差值。 要返回最小差值
                //且k 属于【-k,k】之间
                //可得 趋近于0 和等于0 可以得到最小值 (小于0基本不存在)
                //当 最小值 最大 当 最大值 最小 的时候 得到的差值最小
                //maxNum = maxNum - k  minNum = minNum + k
                //maxNum - k -(minNum + k) = 0
                //当差值大于0或者2k的时候 就是最小差值
                return maxNum - minNum <= 2 * k ? 0 : maxNum - minNum - 2 * k;
            }
        }



//leetcode submit region end(Prohibit modification and deletion)

}
```



`

**输出结果**

![输入图片说明](%E5%9B%BE%E7%89%87/%E6%B5%8B%E8%AF%95%E7%94%A8%E4%BE%8B.png)

**官方测试**

![输入图片说明](%E5%9B%BE%E7%89%87/%E5%AE%98%E6%96%B9%E6%B5%8B%E8%AF%95.png)

