---
layout: post
title: "Java Stream 自定义复杂排序"
author: "Yiru"
tags: 
    - Java
    - 不定期记录
---

#Java Stream 自定义复杂排序

{
    {
        List<Obj> reault = list.stream()
        .sorted(Comparator.comparing(Obj::getValue, (x, y)->{
            //// if(x>y)/////

            return 0; // 1, -1
        }).thenComparing(Comparator.comparing(obj::getPrice, Comparator.nullsFirst(BigDecimal::comparTo)).reversed()))
        .collect(Collectors.toList());        
    }

}


