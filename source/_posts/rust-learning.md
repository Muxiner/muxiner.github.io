---
title: Rust 语言学习历程
math: true
hide: false
date: 2023-04-05 02:01:18
updated: 2023-04-05 02:01:33
excerpt: 无，就是没有。
categories: Learning
tags: Rust
index_img:
banner_img:
sticky: 999
---

## 没有了，该睡觉了，本来是打算简单写写的，结果写 nodejs 安装去了，我敲

## Why 记录

希望有人能够看到吧，避免走弯路。

毕竟总有些傻逼，没做足功课就直接一股脑扎进 rust 学习呢，学了一段时间后，发现，NM，不太对劲，不是很会用的样子，然后找了下，发现还有更加好的教程，或者说是学习路径，还可以边学边练习，还幽默风趣、生动形象、绘声绘色、妙趣横生......还会鼓励咱们，多好呀。

嗯，没错，~~ShaBee is me~~

暂且说这么多。

{% note primary %}
test
{% endnote %}

## LeetCode 刷题学习 Rust

{% note primary %}
更新：2023-04-14 18:31:22
{% endnote %}

### 加一

给定一个由 整数 组成的 非空 数组所表示的非负整数，在该数的基础上加一。

最高位数字存放在数组的首位， 数组中每个元素只存储单个数字。

你可以假设除了整数 0 之外，这个整数不会以零开头。示例：

```txt
输入：digits = [4,3,2,1]
输出：[4,3,2,2]
解释：输入数组表示数字 4321。

输入：digits = [1,2,3]
输出：[1,2,4]
解释：输入数组表示数字 123。

输入：digits = [0]
输出：[1]

1 <= digits.length <= 100
0 <= digits[i] <= 9
```

菜鸟写的，简单直接，有用，但是没啥技巧，我是废物：

```rust
impl Solution {
    pub fn plus_one(digits: Vec<i32>) -> Vec<i32> {
        let mut result: Vec<i32> = Vec::new();
        let mut add = true;
        for i in 0..digits.len() {
            if digits[digits.len() - 1 - i] < 9 && add {
                result.push(digits[digits.len() - 1 - i] + 1);
                add = false;
            } else if digits[digits.len() - 1 - i] == 9 && add {
                result.push(0);
                add = true;
            } else {
                result.push(digits[digits.len() - 1 -i]);
                add = false;
            }
        }
        if add {
            result.push(1);
        }

        let mut return_vec: Vec<i32>= Vec::new();
        
        for i in 0..result.len() {
            return_vec.push(result[result.len() - i - 1]);
        }
        return_vec
    }
}
```

简单描述一下想法：

给咱一个不可变的动态数组 `Vec` 也需要咱们返回一个动态数组 `Vec`，所以是需要咱返回一个新的动态数组。

同时，在过程中发现存在**进位**情况，数组的一个位置只能存 0-9 这十个整数，当尾数 = 9 时，就出现进位情况，那么前一位数字也需要做加法，甚至是出现对 [9,...,9] 做加法的情况，返回的数组就是 [1,0,...,0]，比给的数组长度还多一个。这样的话就需要好好讨论一下了：

+ 不能简单的认为仅仅只需要改变数组最后一位，可能每一位都需要改变
+ 顺序遍历动态数组可能难以实现**每位数字都加一的情况** —— 不好在数组最前面添加内容（存疑，可能是我太废了）
+ 那就需要先倒转数组，然后根据情况来**加一**，使用 `vec.push()` 添加在数组尾部，情况有以下几种：
  1. 仅加一：**个位部分**根据题目要求 + 1；其他的数字因为前一位的进位，而需要做加法
  2. 加一，进位：数字是 9 时，+ 1 后要进位
  3. 保留，不加一，不进位：**除个位部分**没有进位
  4. 是 9...9 这样全是九时，就需要多一个位数。

所以，我的思路：

1. 先创建一个空动态数组
2. 然后将 digits 数组反过来，并根据情况做加法等等
3. 如果数组全是 9 时，还需要加一位
4. 最后再创建一个新的数组，等于处理过的数组反过来
5. 返回结果

结束。

屁，想了下，动态数组可以使用 `Vec::insert()` 函数在任意位置插入元素，那么简单修改一下：

```rust
impl Solution {
    pub fn plus_one(digits: Vec<i32>) -> Vec<i32> {
        let mut add = true;
        let len = digits.len();
        let mut result: Vec<i32> = vec![0; len];

        for i in 0..len {
            let index = len - i - 1;
            if digits[index] == 9 && add {
                result[index] = 0;
                add = true;
            } else if digits[index] < 9 && add {
                result[index] = digits[index] + 1;
                add = false;
            } else {
                result[index] = digits[index];
            }
        }

        if add {
            result.insert(0, 1);
        }

        result
    }
}
```
