---
title: leetcode-5-最长回文字符串的解法
date: 2020-04-05 11:36:18
tags: 
  - leetcode
  - 回文
  - 动态规划
---
<h5>题目：</h5>
给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 <code> s </code>的最大长度为 1000。
<h6>示例一</h6>
```javascript
输入: "babad"
输出: "bab"
注意: "aba" 也是一个有效答案
```
<h6>一.暴力法</h6>
首先就是双重循环，一一遍历的暴力法，直接了当。废话不说，直接上代码。
```javascript
var huiwen = function (s){
    if(s.split('').join()==s.split('').reverse().join()) return true
    return false
}
var longestPalindrome = function(s) {
  if(!s || s.length < 2) return s;
    var ans='';
    var max=0;
    for(let i =0;i<s.length;i++){
        var str=''
        for(let j=i ; j<s.length;j++){
            str+=s[j]
            //console.log(str)
            if(huiwen(str)&&str.length>=max){
                max=str.length
                ans = str
                //console.log(ans)
            }
        }
    }
    return ans
};
```
这是本人自己想的代码，只过了41用例，就超时了，看了看别人的暴力法通过了91用例，道理都差不多，具体应该是str的问题吧。直接到下一种方法<code>动态规划</code>
<h6>二.动态规划</h6>
<br>
<p>由于还不会在博客写公式，先贴一张leetcode的官方题解思路-动态规划</p>
<br>
<img src=/images/leetcode-最长回文字符串动态规划解答.png>
<p>代码如下：</p>
<p>作者：Alexer-660</p>
<span>链接：</span><a href="https://leetcode-cn.com/problems/longest-palindromic-substring/solution/5-zui-chang-hui-wen-zi-chuan-by-alexer-660/">点此直通</a><br>
```javascript
/**
 * @param {string} s
 * @return {string}
 */
var longestPalindrome = function(s) {
    if(!s || s.length < 2){
        return s;
    }
    var s_f = s.split('').reverse().join('');
    var resultStr = s[0];//放结果
    var maxLen = 1;
    var tmpLen = 1;
    var maxStrIndex = 0;//最大下标
    var len = s.length;
    //判断字符串是否回文
    function isPalinerome(i,r){
        if(len - i - 1 == r -tmpLen + 1){
            return true
        }
        return false;
    }
    //初始化二维数组
    var len = s.length;
    var arr = new Array(len);
    for(var i = 0;i<len;i++){
        arr[i] = [];
        for(var r = 0;r<len;r++){
            arr[i][r] = 0
        }
    }
    for(var i = 0;i<len;i++){
        for(var r=0;r<len;r++){
            if(s[i] == s_f[r]){
                if(i==0 || r==0){
                    arr[i][r] = 1
                }else{
                    arr[i][r] = arr[i-1][r-1] + 1
                    tmpLen = arr[i][r]
                }
                if(tmpLen > maxLen && isPalinerome(i,r)){
                    maxStrIndex = r;
                    maxLen = tmpLen;
                    resultStr =  s.substring(i-tmpLen+1,i+1);
                }
            }
        }
    }
    return resultStr;
};
```
运行下来耗时<code>700ms</code>多，占用内存是<code>140MB</code>左右
思路已经明白，就是根据子串的回文性质，转换为求最长子串问题
，这又映射到类似的<a href="https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/">leetcode-3无重复字符的最长子串问题</a>
<p>题目如下：</p>
给定一个字符串，请你找出其中不含有重复字符的 最长子串S的长度。<br>
<h6>示例</h6>
```javascript
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```
<p>在后面博客有讲解：<a href="#">直通</a></p><br>
本次文章到此完毕，谢谢！<span style="float:right">2020/4/4---研究一下动态规划再补充</span>