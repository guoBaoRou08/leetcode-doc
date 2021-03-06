 **每日一题** 

396. 旋转函数
给定一个长度为 n 的整数数组 nums 。

假设 arrk 是数组 nums 顺时针旋转 k 个位置后的数组，我们定义 nums 的 旋转函数  F 为：

F(k) = 0 * arrk[0] + 1 * arrk[1] + ... + (n - 1) * arrk[n - 1]
返回 F(0), F(1), ..., F(n-1)中的最大值 。

生成的测试用例让答案符合 32 位 整数。

 

示例 1:

输入: nums = [4,3,2,6]
输出: 26
解释:

F(0) = (0 * 4) + (1 * 3) + (2 * 2) + (3 * 6) = 0 + 3 + 4 + 18 = 25
F(1) = (0 * 6) + (1 * 4) + (2 * 3) + (3 * 2) = 0 + 4 + 6 + 6 = 16
F(2) = (0 * 2) + (1 * 6) + (2 * 4) + (3 * 3) = 0 + 6 + 8 + 9 = 23
F(3) = (0 * 3) + (1 * 2) + (2 * 6) + (3 * 4) = 0 + 2 + 12 + 12 = 26
所以 F(0), F(1), F(2), F(3) 中的最大值是 F(3) = 26 。
示例 2:

输入: nums = [100]
输出: 0
 

提示:

n == nums.length
1 <= n <= 105
-100 <= nums[i] <= 100

 **题干截图** 

![输入图片说明](%E5%9B%BE%E7%89%87/%E6%AF%8F%E6%97%A5%E4%B8%80%E9%A2%98.png)

 **代码分析** 

根据推导公式如图：

![输入图片说明](%E5%9B%BE%E7%89%87/%E6%8E%A8%E5%88%B0%E5%85%AC%E5%BC%8F.png)

利用公式将变量带入可得:

 **代码截图** 

![输入图片说明](%E5%9B%BE%E7%89%87/%E8%AF%A6%E7%BB%86%E4%BB%A3%E7%A0%81.png)

 **解题源码** 

```
//给定一个长度为 n 的整数数组 nums 。 
//
// 假设 arrk 是数组 nums 顺时针旋转 k 个位置后的数组，我们定义 nums 的 旋转函数 F 为： 
//
// 
// F(k) = 0 * arrk[0] + 1 * arrk[1] + ... + (n - 1) * arrk[n - 1] 
// 
//
// 返回 F(0), F(1), ..., F(n-1)中的最大值 。 
//
// 生成的测试用例让答案符合 32 位 整数。 
//
// 
//
// 示例 1: 
//
// 
//输入: nums = [4,3,2,6]
//输出: 26
//解释:
//F(0) = (0 * 4) + (1 * 3) + (2 * 2) + (3 * 6) = 0 + 3 + 4 + 18 = 25
//F(1) = (0 * 6) + (1 * 4) + (2 * 3) + (3 * 2) = 0 + 4 + 6 + 6 = 16
//F(2) = (0 * 2) + (1 * 6) + (2 * 4) + (3 * 3) = 0 + 6 + 8 + 9 = 23
//F(3) = (0 * 3) + (1 * 2) + (2 * 6) + (3 * 4) = 0 + 2 + 12 + 12 = 26
//所以 F(0), F(1), F(2), F(3) 中的最大值是 F(3) = 26 。
// 
//
// 示例 2: 
//
// 
//输入: nums = [100]
//输出: 0
// 
//
// 
//
// 提示: 
//
// 
// n == nums.length 
// 1 <= n <= 105 
// -100 <= nums[i] <= 100 
// 
// Related Topics 数组 数学 动态规划 
// 👍 139 👎 0

package leetcode.editor.cn;

import java.util.Arrays;
import java.util.List;

//Java：旋转函数
 class P396RotateFunction{
    public static void main(String[] args) {
        Solution solution = new P396RotateFunction().new Solution();
        // TO TEST
        List<Integer> setList = Arrays.asList(4,2,45,52,3);
        int[] arr = setList.stream().mapToInt(i -> i).toArray(); //[1, 2, 3, 4]
        System.out.println("输入数组："+setList);
        System.out.println("输出最大结果："+solution.maxRotateFunction(arr));
        //solution.maxRotateFunction(setList);
    }
    //leetcode submit region begin(Prohibit modification and deletion)
class Solution {
        public int maxRotateFunction(int[] nums) {
            //初始开始数组长度，推导公式临时总计数sum
            int numsLength = nums.length, sum = 0;
            //初始分F[0]总计数
            int initSum = 0;
            //循环获得原始数组总计数和初始F[0]总计数
            for (int i = 0; i < numsLength; i++) {
                sum += nums[i];
                initSum += i * nums[i];
            }
            //目标结果最少是初始数组计数并赋值
            int res = initSum;
            //初始从1开始因为 由推到公式从n-1 则循环从1开始循环
            for (int i = 1; i < numsLength; i++) {
                //根据推导公式赋值相关变量
                int nextSum = initSum + sum - numsLength * nums[numsLength - i];
                //依次比较最大值
                res = Math.max(res, nextSum);
                //赋初始计数值
                initSum = nextSum;
            }
            //返结果
            return res;
        }
}
//leetcode submit region end(Prohibit modification and deletion)

}
```

 **输出结果** 

![输入图片说明](%E5%9B%BE%E7%89%87/%E8%BE%93%E5%87%BA%E7%BB%93%E6%9E%9C.png)

 **官方测试** 

![输入图片说明](%E5%9B%BE%E7%89%87/%E5%AE%98%E6%96%B9%E6%B5%8B%E8%AF%95.png)