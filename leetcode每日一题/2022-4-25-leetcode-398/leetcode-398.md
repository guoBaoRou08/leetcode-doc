**每日一题**

#### [398. 随机数索引](https://leetcode-cn.com/problems/random-pick-index/)

难度中等194收藏分享切换为英文接收动态反馈

给定一个可能含有重复元素的整数数组，要求随机输出给定的数字的索引。 您可以假设给定的数字一定存在于数组中。

**注意：**
数组大小可能非常大。 使用太多额外空间的解决方案将不会通过测试。

**示例:**

```
int[] nums = new int[] {1,2,3,3,3};
Solution solution = new Solution(nums);

// pick(3) 应该返回索引 2,3 或者 4。每个索引的返回概率应该相等。
solution.pick(3);

// pick(1) 应该返回 0。因为只有nums[0]等于1。
solution.pick(1);
```



**题干截图**

![输入图片说明](%E5%9B%BE%E7%89%87/%E6%AF%8F%E6%97%A5%E4%B8%80%E9%A2%98.png)

**代码分析**

分析图引用大佬的图，图画的很到位。

> 出处：https://leetcode-cn.com/problems/linked-list-random-node/solution/xu-shui-chi-chou-yang-suan-fa-sha-zi-du-neng-kan-d/

![输入图片说明](%E5%9B%BE%E7%89%87/%E5%88%86%E6%9E%901.png)

![输入图片说明](%E5%9B%BE%E7%89%87/%E5%88%86%E6%9E%902.png)

![输入图片说明](%E5%9B%BE%E7%89%87/%E5%88%86%E6%9E%903.png)

![输入图片说明](%E5%9B%BE%E7%89%87/%E5%88%86%E6%9E%904.png)


根据测试用例：

输入：[3, 5, 5]
输出：2

由测试用例知道m=1，N=2

 **解析：** 

第一项在[0,1)中m=1,取等于0的概率为1，直接放入

第一项不被替换就是不被第二项替换

概率为(1-1/2*1)*(1-1/2*1)*1 = 1/2*1 =1/2

即第一项被选中的概率为1/2


第二项在[0,2)中选到的随机数大于m，被选入蓄水池的概率为m/i = 1/2

第二项后面没有了，所以没有被替换的风险

第二项被选中的概率为1/2



注：如果N等于3.4.5或以此类推 带入公式

![输入图片说明](%E5%9B%BE%E7%89%87/%E5%88%86%E6%9E%905.png)

**代码截图**

![输入图片说明](%E5%9B%BE%E7%89%87/%E4%BB%A3%E7%A0%81%E8%A7%A3%E5%9B%BE1.png)
![输入图片说明](%E5%9B%BE%E7%89%87/%E4%BB%A3%E7%A0%81%E8%A7%A3%E5%9B%BE2.png)


**解题源码**


```
package leetcode.editor.cn;

import java.util.Arrays;
import java.util.Random;

//Java：随机数索引
 class P398RandomPickIndex{
    public static void main(String[] args) {
        int[] nums = {3,5,5};
        Solution solution = new P398RandomPickIndex().new Solution(nums);
        // TO TEST
        int pikNum = solution.pick(5);
        System.out.println("输入：" + Arrays.toString(nums) );
        System.out.println("输出：" + pikNum );
    }
    //leetcode submit region begin(Prohibit modification and deletion)
    class Solution {
        int[] nums;
        Random random;
        //构造函数初始化数据
        public Solution(int[] nums) {
            this.nums = nums;
            random = new Random();
        }
        //调用获取目标随机下标索引
        public int pick(int target) {
            int res = 0;
            //初始循环起始i，meetCnt,循环遍历数组长度
            for (int i = 0, meetCnt = 0; i < nums.length; ++i) {
                //每层遍历当与目标数相等时候判断
                if (nums[i] == target) {
                    ++meetCnt; // 第 meetCnt 次遇到 target meetCnt 加1
                    //获取随机[0,meetCnt)是否得0 则可等到 1/meetCnt 概率
                    if (random.nextInt(meetCnt) == 0) {
                        //小标索引赋值
                        res = i;
                    }
                }
            }
            //返回索引下标
            return res;
        }
    }


/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(nums);
 * int param_1 = obj.pick(target);
 */
//leetcode submit region end(Prohibit modification and deletion)

}
```

**输出结果**

![输入图片说明](%E5%9B%BE%E7%89%87/%E6%B5%8B%E8%AF%95%E7%94%A8%E4%BE%8B.png)


**官方测试**

![输入图片说明](%E5%9B%BE%E7%89%87/%E5%AE%98%E6%96%B9%E6%B5%8B%E8%AF%95.png)

![输入图片说明](%E5%9B%BE%E7%89%87/%E5%AE%98%E6%96%B9%E6%B5%8B%E8%AF%952.png)

