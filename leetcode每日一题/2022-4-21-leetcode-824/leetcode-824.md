 **每日一题** 


- 824. 山羊拉丁文
- 给你一个由若干单词组成的句子 sentence ，单词间由空格分隔。每个单词仅由大写和小写英文字母组成。
- 请你将句子转换为 “山羊拉丁文（Goat Latin）”（一种类似于 猪拉丁文 - Pig Latin 的虚构语言）。山羊拉丁文的规则如下：
- 如果单词以元音开头（'a', 'e', 'i', 'o', 'u'），在单词后添加"ma"。
- 例如，单词 "apple" 变为 "applema" 。
- 如果单词以辅音字母开头（即，非元音字母），移除第一个字符并将它放到末尾，之后再添加"ma"。
- 例如，单词 "goat" 变为 "oatgma" 。
- 根据单词在句子中的索引，在单词最后添加与索引相同数量的字母'a'，索引从 1 开始。
- 例如，在第一个单词后添加 "a" ，在第二个单词后添加 "aa" ，以此类推。
- 返回将 sentence 转换为山羊拉丁文后的句子。

 
示例 1：

输入：sentence = "I speak Goat Latin"

输出："Imaa peaksmaaa oatGmaaaa atinLmaaaaa"

示例 2：

输入：sentence = "The quick brown fox jumped over the lazy dog"

输出："heTmaa uickqmaaa rownbmaaaa oxfmaaaaa umpedjmaaaaaa overmaaaaaaa hetmaaaaaaaa azylmaaaaaaaaa ogdmaaaaaaaaaa"

提示：

1 <= sentence.length <= 150
sentence 由英文字母和空格组成
sentence 不含前导或尾随空格
sentence 中的所有单词由单个空格分隔

 **题干截图** 

![输入图片说明](%E5%9B%BE%E7%89%87/%E6%AF%8F%E6%97%A5%E4%B8%80%E9%A2%98.png)

 **代码分析** 

根据题干模拟带入变量，循环判断。

 **代码截图** 

![输入图片说明](%E5%9B%BE%E7%89%87/%E8%A7%A3%E9%A2%981.png)

![输入图片说明](%E5%9B%BE%E7%89%87/%E8%A7%A3%E9%A2%982.png)

 **解题源码** 

```
//给你一个由若干单词组成的句子 sentence ，单词间由空格分隔。每个单词仅由大写和小写英文字母组成。 
//
// 请你将句子转换为 “山羊拉丁文（Goat Latin）”（一种类似于 猪拉丁文 - Pig Latin 的虚构语言）。山羊拉丁文的规则如下： 
//
// 
// 如果单词以元音开头（'a', 'e', 'i', 'o', 'u'），在单词后添加"ma"。
//
// 
// 例如，单词 "apple" 变为 "applema" 。 
// 
// 
// 如果单词以辅音字母开头（即，非元音字母），移除第一个字符并将它放到末尾，之后再添加"ma"。
// 
// 例如，单词 "goat" 变为 "oatgma" 。 
// 
// 
// 根据单词在句子中的索引，在单词最后添加与索引相同数量的字母'a'，索引从 1 开始。
// 
// 例如，在第一个单词后添加 "a" ，在第二个单词后添加 "aa" ，以此类推。 
// 
// 
// 
//
// 返回将 sentence 转换为山羊拉丁文后的句子。 
//
// 
//
// 示例 1： 
//
// 
//输入：sentence = "I speak Goat Latin"
//输出："Imaa peaksmaaa oatGmaaaa atinLmaaaaa"
// 
//
// 示例 2： 
//
// 
//输入：sentence = "The quick brown fox jumped over the lazy dog"
//输出："heTmaa uickqmaaa rownbmaaaa oxfmaaaaa umpedjmaaaaaa overmaaaaaaa hetmaaaaa
//aaa azylmaaaaaaaaa ogdmaaaaaaaaaa"
// 
//
// 
//
// 提示： 
//
// 
// 1 <= sentence.length <= 150 
// sentence 由英文字母和空格组成 
// sentence 不含前导或尾随空格 
// sentence 中的所有单词由单个空格分隔 
// 
// Related Topics 字符串 
// 👍 70 👎 0

package leetcode.editor.cn;

import java.util.*;

//Java：山羊拉丁文
 class P824GoatLatin{
    public static void main(String[] args) {
        Solution solution = new P824GoatLatin().new Solution();
        // TO TEST
        String inPut = "asd sad vd SD vf SDSD asd";
        System.out.println("输入：" + inPut);
        System.out.println("输出：" + solution.toGoatLatin(inPut));

    }
    //leetcode submit region begin(Prohibit modification and deletion)
    class Solution {

        //给元音建立数组存留私有不可变
        private  final List<Character> setList = Arrays.asList('a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U');

        public String toGoatLatin(String s) {
            //对入参字符串以空格分割成数组
            String[] array = s.split(" ");
            //new初始化数组，用作存放每一个处理后字符
            List<String> ans = new ArrayList<>();

            //对数组array循环遍历对每一个子字符处理
            for (int i = 0; i < array.length; i++) {
                //新建立string类
                StringBuilder sb = new StringBuilder();
                //每次获取数组中字符
                String str = array[i];
                //从元音数组中取出判断str第一个字符是否为元音
                if (setList.contains(str.charAt(0))) {
                    sb.append(str);//纯在则直接拼接
                } else {
                    //判断第一个字符不为元音，是以辅音字母开头
                    sb.append(str.substring(1)); //截取从第一个字符后开始拼接
                    sb.append(str.charAt(0));//末尾添加第一个字符
                }
                //全都添加ma
                sb.append("ma");
                //循环遍历添加与索引相同的‘a’
                for (int j = 0; j < i + 1; j++) {
                    sb.append('a');
                }
                //向数组添加每一个处理后的元素
                ans.add(sb.toString());
            }
            //把数组转换成字符串用“ ” 分割
            return String.join(" ", ans);
        }
    }



//leetcode submit region end(Prohibit modification and deletion)

}
```
 **输出结果** 

![输入图片说明](%E5%9B%BE%E7%89%87/%E8%BE%93%E5%87%BA1.png)


 **官方测试** 

![输入图片说明](%E5%9B%BE%E7%89%87/%E8%BE%93%E5%87%BA2.png)
