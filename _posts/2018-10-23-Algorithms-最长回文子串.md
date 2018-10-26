---
layout: post
title: "如何找到字符串中的最长回文子串"
author: "Yiru"
tags: 
    - 算法
    - 每日修行
---

#如何找到字符串中的最长回文子串

回文字符串是前后读完全一致的字符串. 所以, 第一反应是,用一个栈: 依次遍历字符串入栈, 匹配的话,就出栈.

但是回文字符串有两种: 
- abccba -- 偶数个
- abcba  -- 奇数个

当遇到偶数回文的话, 可以在栈顶匹配. 如果是奇数个回文字符串的话, 就需要出栈两个了.


1.  定义一个栈
2.  定义一个List<String> 用来存储找到的回文字符串
3.  定义2个临时字符变量, 一个放栈顶字符 top. 
4.  遍历字符串, 将字符串放入top中,
    然后,字符串依次入栈.
    
    读取下一个的时候, 匹配top, 如果不相同, 匹配栈顶字符.

    如果都不相同, 将top入栈, 新字符存入top中.

    如果相同, 定义一个新的临时字符串, 将两个字符前后各一拼接起来.再取下一个.

    当某一个字符不匹配时, 将这个临时字符串入栈. 
    
    —— 这是因为有可能某个子回文串, 是另一个的一部分: abccbebccba

    依次进行操作,直到遍历完所有的字符串.


5.  list中, 最长的一个,就是寻找到的最长的回文子串.


======================================

不对不对, 可以不用栈,只要用一直遍历就可以, 需要两个指针记录位置, 一个用来遍历, 一个用来匹配.

{
package com.yiru.study.algorithms.strings;

public class TheLongestedPalindrome {

    public static void main(String[] args) {

        String source = "aacbaabcbebcbaabcjkl";
        System.out.println(TheLongestedPalindrome.find(source));
    }

    public static String find(String source) {

        int length = source.length();
        if (length < 2) {
            return "";
        }

        int start = 0;
        int end = 0;
        if (source.charAt(0) == source.charAt(1)) { // 不想每次都要判断是不是>2
            start = 0;
            end = 2;
        }
        int max = end - start;

        int index = 2;
        int match;

        while (index < length) {
            match = index - 1;
            if (source.charAt(index) != source.charAt(match)) {// 判断第一个是不是相等
                match--; // 如果不相等, 匹配下一个
            }
            // ! 这里忘记了, 也需要添加一个校验
            while ((index < length )&& (match >=0) && (source.charAt(index) == source.charAt(match))) {{ //一直匹配, 直到不同为止.
                index++;
                match--;
            }

            int len = index - match - 2; //计算长度. 如果没有匹配成功, len=0
            if (len > max) { // max初始值为0. 如果比当前长, 存储.
                max = len;
                end = --index; // index 回退一个
                start = match + 1;
            }
            index++; // 继续下一个.
        }

        return source.substring(start, end);
    }

}
}


input:aacbaabcbebcbaabcjkl

output:cbaabcbebcbaab

回文字符串:
aa

cbaabc

bcb

cbaabcbebcbaabc

一次成功!


=========================================================

看一看,我觉得,我的方案更优化,哈哈哈!







