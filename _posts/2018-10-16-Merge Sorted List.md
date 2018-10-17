---
layout: post
title: "Merge Two sorted lists"
author: "Yiru"
tags: 
    - 每日修行
    - 算法
---


Merge Two sorted lists

Merge two sorted linked lists and return it as a new list. 
The new list should be made by splicing together the nodes of the first two lists.

Example:

Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4

提示：提交代码后，需要用简洁的语言解释一下代码思路~




public static void main(String[] args){
    List<Integer> list1 = Arrays.asList(1,3,5,7,9);
    List<Integer> list2 = Arrays.asList(2,4,6,8);

    int[] result = new int[list1.size() + list2.size()];

    int i = 0;
    int idx1 = 0;
    int idx2 = 0;

    while(true)
    {
        if (idx1 == list1.size() && idx2 == list2.size()) {
            break;
        }
        int tmp=0;
        if (idx2 == list2.size() || list1.get(idx1) < list2.get(idx2)) {
            tmp = list1.get(idx1++);
        } else if (idx1 == list1.size() || list1.get(idx1) >= list2.get(idx2)) {
            tmp = list2.get(idx2++);
        }
        System.out.print(tmp + "\t");
        result[i++] = tmp;
    }
    
}

这个还是很简单的.
