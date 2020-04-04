---
title: leetcode-6-Z字形变换
date: 2020-04-04 14:20:29
tags: leetcode
---

<h5>题目描述</h5>
将一个给定字符串根据给定的行数，以从上往下、从左到右进行 Z 字形排列。
比如输入字符串为 "LEETCODEISHIRING" 行数为 3 时，排列如下：
```javascript
L   C   I   R
E T O E S I I G
E   D   H   N
```
之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如：<code>"LCIRETOESIIGEDHN"</code>。
请你实现这个将字符串进行指定行数变换的函数：
<code>string convert(string s, int numRows);</code>
<h5>示例1：</h5>
```
输入: s = "LEETCODEISHIRING", numRows = 4
输出: "LDREOEIIECIHNTSG"
解释:

L     D     R
E   O E   I I
E C   I H   N
T     S     G
```
上面是题目的基本介绍，拿到这道题我的思路首先是遍历字符串，但是字符串排列规律一时间不好确定，
于是通过画图来看，本来思路是创建一个二维数组往进去填字符串，然后最后按行拼接，去除空的就像，然鹅并没有写出填的方法。于是乎打开了leetcode的题解，膜拜了一下大神的写法。先上代码：
对于大神的代码每行注释以下方便理解
```javascript
var convert = function(s, numRows) {
    if(numRows == 1)
        return s;//向来函数第一先边界判断！！！

    const len = Math.min(s.length, numRows);//取字符串长度和Z高的较小值
    //console.log("len=" +len)//输出一下(此行我加的--忽略)
    const rows = [];
    for(let i = 0; i< len; i++) rows[i] = "";
    //console.log(rows)
    let loc = 0;
    let down = false;

    for(const c of s) {
        rows[loc] += c;
        if(loc == 0 || loc == numRows - 1)
            down = !down;
        loc += down ? 1 : -1;
    }

    let ans = "";
    for(const row of rows) {
        ans += row;
    }
    return ans;
};
console.log(convert("LEETCODEISHIRING",3))
```
图解如下：<a href="https://leetcode-cn.com/problems/zigzag-conversion/solution/hua-jie-suan-fa-6-z-zi-xing-bian-huan-by-guanpengc/">转自leetcode</a>
<img src=/images/Z字形变换图解.png>
这样的解法就是把直接按行输出字符串，无中间空余，作者设了一个down参量来判断是否是“Z”的竖列，每次给<code>rows[0]rows[1]rows[2]......rows[n]</code>字符串值拼接即可得到答案，感觉很巧妙，关键在与rows的设置和down的运用。其他算法相比这个较复杂，这个好理解，等我发现更好的，或者通法再来补充。
<a href="https://leetcode-cn.com/u/guanpengchn/">感谢这位leetcode名为灵魂画手作者的奉献</a>









