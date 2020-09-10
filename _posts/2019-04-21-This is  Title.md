---
layout:     post
title:      Leetcode1577
subtitle:   Number of Ways Where Square of Number Is Equal to Product of Two Numbers
date:       2020-09-10
author:     SY
header-img: img/post-bg-swift2.jpg
catalog: true
tags:
    - Leetcode
    - HashMap
---
This question is from Leetcode weekly contest 205.

# O(N^2) PrevCalculate

```Java
class Solution {
    public int numTriplets(int[] nums1, int[] nums2) {
        Map<Integer, Map<Integer, Integer>> map1 = new HashMap();
        for(int i = 0; i < nums1.length; i++){
            map1.put(i, new HashMap());
            for(int j = i + 1; j < nums1.length; j++){
                map1.get(i).put(nums1[j], map1.get(i).getOrDefault(nums1[j], 0) + 1);
            }
        }
        Map<Integer, Map<Integer, Integer>> map2 = new HashMap();
        for(int i = 0; i < nums2.length; i++){
            map2.put(i, new HashMap());
            for(int j = i + 1; j < nums2.length; j++){
                map2.get(i).put(nums2[j], map2.get(i).getOrDefault(nums2[j], 0) + 1);
            }
        }
        int res = 0;
        for(int i = 0; i < nums1.length; i++){
            long curr = nums1[i], target = curr * curr;
            for(int j = 0; j < nums2.length; j++){
                if(target % nums2[j] == 0 && map2.get(j).containsKey((int)(target / nums2[j]))){
                    res += map2.get(j).get((int)(target / nums2[j]));
                }
            }
        }
        for(int i = 0; i < nums2.length; i++){
            long curr = nums2[i], target = curr * curr;
            for(int j = 0; j < nums1.length; j++){
                if(target % nums1[j] == 0 && map1.get(j).containsKey((int)(target / nums1[j]))){
                    res += map1.get(j).get((int)(target / nums1[j]));
                } 
            }
        }
        return res;
    }
}
```
