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


## Why 记录

希望有人能够看到吧，避免走弯路。

毕竟总有些傻逼，没做足功课就直接一股脑扎进 rust 学习呢，学了一段时间后，发现，NM，不太对劲，不是很会用的样子，然后找了下，发现还有更加好的教程，或者说是学习路径，还可以边学边练习，还幽默风趣、生动形象、绘声绘色、妙趣横生......还会鼓励咱们，多好呀。

嗯，没错，~~ShaBee is me~~

暂且说这么多。

## Rust 环境

### vscode rust 插件

+ `rust-analyzer`：社区驱动的 Rust 语言的插件，就是好用。
+ `Even Better TOML`：支持 .toml 文件完整特性
+ `Error Lens`：更好的获得错误展示
+ `CodeLLDB`：Debugger 程序

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

{% note info %}
还有这个可以学习。
在 Rust 中，.rev()是一个方法，它返回一个反转（reverse）迭代器。该方法可以应用于任何实现了 std::iter::Iterator trait 的对象。调用 .rev() 方法后，将返回一个产生与原始迭代器相同元素，但顺序相反的迭代器。在给定示例代码中，.rev() 用于将索引从大到小遍历。

在这个例子中，for i in (0..digits.len()).rev() 意味着 i 变量将从 digits 中最后一个元素的索引开始（即 digits.len() - 1），并递减到第一个元素的索引（即 0）。

有个骚逼炫技，真他妈的骚，代码格式也不好好搞：

+ 是指除了题目给定的有指令的行数。
+ 用的是“数 9 法”，先找出从右到左第一个非9的下标i，然后懂的都懂。
+ None表示全都是 9！
+ `[a,b,c].concat()` 表示将 a, b ,c 三个切片连城一个Vec数组。

```rust
impl Solution {
    pub fn plus_one(digits: Vec<i32>) -> Vec<i32> {
        match digits
            .iter()
            .enumerate()
            .rev()
            .skip_while(|(i, &x)| 9 == x)
            .next()
        {
            Some((i, &a)) => [
                digits[..i]
                    .iter()
                    .map(|x| x.clone())
                    .collect::<Vec<i32>>()
                    .as_slice(),
                vec![digits[i] + 1].as_slice(),
                vec![0; digits.len() - (i + 1)].as_slice(),
            ]
            .concat(),
            None => [vec![1].as_slice(), vec![0; digits.len()].as_slice()].concat(),
        }
    }
}
```

{% endnote %}


## Rust 小练习 —— rustlings

项目地址：[rust-lang/rustlings: Small exercises to get you used to reading and writing Rust code!](https://github.com/rust-lang/rustlings)

中文项目地址：[rust-lang-cn/rustlings-cn: Rustlings 非官方中文翻译(Rustlings unofficial chinese verion)。🦀 让你熟悉阅读和编写 Rust 代码的小练习。源仓库：https://github.com/rust-lang/rustlings](https://github.com/rust-lang-cn/rustlings-cn)

项目作用：Rust 小练习，Rust 官方推出的交互式练习工具，边阅读、修改和运行代码，边学习概念。

### 简单开始

### 难题记录

#### exercises/error_handling/errors6.rs

题目链接：[exercises/error_handling/errors6.rs](https://github.com/rust-lang/rustlings/blob/main/exercises/error_handling/errors6.rs)
非官方翻译题目链接：[exercises/error_handling/errors6.rs](https://github.com/rust-lang-cn/rustlings-cn/blob/main/exercises/error_handling/errors6.rs)

```rust
// errors6.rs

// 使用能够捕获所有错误的类型，比如说 `Box<dyn error::Error>`，在库代码中是不推荐的，
// 其调用者可能想要基于错误的内容做决定，而不是将错误打印出来或向前传播。
// 这里，我们定义了一个自定义错误类型，使调用者在我们的函数返回错误时做判断成为可能。

// 执行 `rustlings hint errors6` 或在观察模式下使用 `hint` 子命令来获取提示。

// I AM NOT DONE

use std::num::ParseIntError;

// 这是一个我们将会在 `parse_pos_nonzero()` 用到的自定义错误类型。
#[derive(PartialEq, Debug)]
enum ParsePosNonzeroError {
    Creation(CreationError),
    ParseInt(ParseIntError),
}

impl ParsePosNonzeroError {
    fn from_creation(err: CreationError) -> ParsePosNonzeroError {
        ParsePosNonzeroError::Creation(err)
    }
    // TODO: 在这里添加另一个错误转换函数。
    // fn from_parseint...
}

fn parse_pos_nonzero(s: &str) -> Result<PositiveNonzeroInteger, ParsePosNonzeroError> {
    // TODO: 改变这里以返回一个适当的错误，而不是在
    // `parse()` 返回错误时发生 panic。
    let x: i64 = s.parse().unwrap();
    PositiveNonzeroInteger::new(x).map_err(ParsePosNonzeroError::from_creation)
}

// 不要改变这行以下的任何东西。

#[derive(PartialEq, Debug)]
struct PositiveNonzeroInteger(u64);

#[derive(PartialEq, Debug)]
enum CreationError {
    Negative,
    Zero,
}

impl PositiveNonzeroInteger {
    fn new(value: i64) -> Result<PositiveNonzeroInteger, CreationError> {
        match value {
            x if x < 0 => Err(CreationError::Negative),
            x if x == 0 => Err(CreationError::Zero),
            x => Ok(PositiveNonzeroInteger(x as u64)),
        }
    }
}

#[cfg(test)]
mod test {
    use super::*;

    #[test]
    fn test_parse_error() {
        // 我们不能构造一个 ParseIntError，所以只能进行模式匹配。
        assert!(matches!(
            parse_pos_nonzero("not a number"),
            Err(ParsePosNonzeroError::ParseInt(_))
        ));
    }

    #[test]
    fn test_negative() {
        assert_eq!(
            parse_pos_nonzero("-555"),
            Err(ParsePosNonzeroError::Creation(CreationError::Negative))
        );
    }

    #[test]
    fn test_zero() {
        assert_eq!(
            parse_pos_nonzero("0"),
            Err(ParsePosNonzeroError::Creation(CreationError::Zero))
        );
    }

    #[test]
    fn test_positive() {
        let x = PositiveNonzeroInteger::new(42);
        assert!(x.is_ok());
        assert_eq!(parse_pos_nonzero("42"), Ok(x.unwrap()));
    }
}
```

本题主要修改两处地方，即 `TODO` ：

```rust
impl ParsePosNonzeroError {
    fn from_creation(err: CreationError) -> ParsePosNonzeroError {
        ParsePosNonzeroError::Creation(err)
    }
    // TODO: 在这里添加另一个错误转换函数。
    // fn from_parseint...
}

fn parse_pos_nonzero(s: &str) -> Result<PositiveNonzeroInteger, ParsePosNonzeroError> {
    // TODO: 改变这里以返回一个适当的错误，而不是在
    // `parse()` 返回错误时发生 panic。
    let x: i64 = s.parse().unwrap();
    PositiveNonzeroInteger::new(x).map_err(ParsePosNonzeroError::from_creation)
}
```

解题思路：

根据测试函数中的内容，调用的 `parse_pos_nonzero()` 函数，接受一个字符串参数，返回 `Ok` 或 `Err` 的情况，且 `Err` 还有不同的类型，如：

+ `Err(ParsePosNonzeroError::Creation(CreationError::Negative))`
+ `Err(ParsePosNonzeroError::Creation(CreationError::Zero))`
+ `Err(ParsePosNonzeroError::ParseInt(_))`

共三种类型。

第一个 `TODO` 需要实现**另一个错误转换函数** —— `from_parseint()`，转换为 `ParsePosNonzeroError::ParseInt(err)` 类型。

参考前文的 `from_creation()` 方法:

```rust
fn from_creation(err: CreationError) -> ParsePosNonzeroError {
        ParsePosNonzeroError::Creation(err)
}
```

照葫芦画瓢即可：

```rust
fn from_parseint(err: ParseIntError) -> ParsePosNonzeroError {
    ParsePosNonzeroError::ParseIntError(err)
}
```

第二个 `TODO` 处检查发现是没有返回 `Err(ParsePosNonzeroError::ParseInt(_))`，即接收 `"not a number"` 等非数字的字符串时，无法正常转换成整数，需要返回一个错误转换的错误信息。

而原题中可正常转换 `"123"`、`"0"`、`"-555"` 等正常的整数情况从而返回：

+ `Ok(PositiveNonzeroInteger(u64))`
+ `Err(ParsePosNonzeroError::Creation(CreationError::Zero))`
+ `Err(ParsePosNonzeroError::Creation(CreationError::Negative))`

三个 `Ok` 和 `Err` 的信息。

未修改的代码的测试结果为：

```rust
thread 'test::test_parse_error' panicked at 'called `Result::unwrap()` on an `Err` value: ParseIntError { kind: InvalidDigit }',
```

解释为：测试函数 `test_parse_error` 调用 `parse_pos_nonzero` 函数时，字符串转换出错 —— 调用 `Result::unwrap()` 函数时接收了一个 `Err(ParseIntError::InvalidDigit)`，这就出错了:

```rust
#[test]
fn test_parse_error() {
    assert!(matches!(
        parse_pos_nonzero("not a number"),
        Err(ParsePosNonzeroError::ParseInt(_))
    ));
}
```

查阅 Rust 官方标准库 —— `Struct std::num::ParseIntError`，地址：[Struct std::num::ParseIntError | 中文](https://rustwiki.org/zh-CN/std/num/struct.ParseIntError.html)，并查看其[源码内容](https://rustwiki.org/zh-CN/src/core/num/error.rs.html#69-71)，可知 `ParseIntError::InvalidDigit` 表示**在其上下文中包含无效数字** —— 除其他原因外，当解析包含非 ASCII 字符的字符串时，将创建这个变体。当 `+` 或 `-` 单独放置在字符串中或放置在数字中间时，也会创建此变体。

而 `std::result::Result` 的 `unwrap()` 方法是返回包含 `self` 值的包含的 `Ok` 值:

```txt
返回包含 self 值的包含的 Ok 值。

由于此函数可能为 panic，因此通常不建议使用该函数。 相反，更喜欢使用模式匹配并显式处理 Err 大小写，或者调用 unwrap_or，unwrap_or_else 或 unwrap_or_default。

Panics
如果该值为 Err，就会出现 Panics，并由 Err 的值提供 panic 消息。
```

所以，不应当使用 `unwrap()` 方法了。可以使用**匹配**或者 `map_err()` 方法进行处理。

```txt
pub fn map_err<F, O>(self, op: O) -> Result<T, F>

通过对包含的 Err 值应用函数，将 Ok 值 Maps 转换为 Result<T, F>，而保持 Ok 值不变。

此函数可用于在处理错误时传递成功的结果。
```

##### 答案

故而对于 `parse_pos_error()` 函数的修改方案有如下几种：

**分情况进行嵌套匹配**

```rust
fn parse_pos_nonzero(s: &str) -> Result<PositiveNonzeroInteger, ParsePosNonzeroError> {
    match s.parse() {
        Ok(x) => {
            match PositiveNonzeroInteger::new(x) {
                Ok(PositiveNonzeroInteger(x)) => Ok(PositiveNonzeroInteger(x)),
                Err(CreationError::Zero) => Err(ParsePosNonzeroError::from_creation(CreationError::Zero)),
                Err(CreationError::Negative) => Err(ParsePosNonzeroError::from_creation(CreationError::Negative)),
            }
        },
        Err(ParseIntError) => Err(ParsePosNonzeroError::from_parseint(ParseIntError)),
    }
}
```

或者稍微简化一下代码 —— 使用 `message` 表示 `Ok` 或 `Err` 中的内容：

```rust
fn parse_pos_nonzero(s: &str) -> Result<PositiveNonzeroInteger, ParsePosNonzeroError> {
    match s.parse() {
        Ok(x) => {
            match PositiveNonzeroInteger::new(x) {
                Ok(message) => Ok(message),
                Err(message) => Err(ParsePosNonzeroError::from_creation(message)),
            }
        },
        Err(message) => Err(ParsePosNonzeroError::from_parseint(message)),
    }
}
```

**使用 `map_err()` 和 嵌套匹配**

```rust
fn parse_pos_nonzero(s: &str) -> Result<PositiveNonzeroInteger, ParsePosNonzeroError> {
    match s.parse() {
        Ok(x) => PositiveNonzeroInteger::new(x).map_err(ParsePosNonzeroError::from_creation),
        Err(err) => Err(ParsePosNonzeroError::from_parseint(err)),
    }
}
```

或者是直接返回 `Err(ParsePosNonzeroError::ParseInt(err))`:

```rust
fn parse_pos_nonzero(s: &str) -> Result<PositiveNonzeroInteger, ParsePosNonzeroError> {
    match s.parse() {
        Ok(x) => PositiveNonzeroInteger::new(x).map_err(ParsePosNonzeroError::from_creation),
        Err(err) => Err(ParsePosNonzeroError::ParseInt(err)),
    }
}
```

**第三种方法，使用 `?` 操作符使函数提前返回和使用 `map_err()` 方法**

```rust
fn parse_pos_nonzero(s: &str) -> Result<PositiveNonzeroInteger, ParsePosNonzeroError> {
    let x: i64 = s.parse().map_err(ParsePosNonzeroError::from_parseint)?;
    PositiveNonzeroInteger::new(x).map_err(ParsePosNonzeroError::from_creation)
}
```

简单说就是，当时转换失败时，使用 map_err() 方法处理 `ParsePosNonzeroError::ParseInt(err)` 并使用 `?` 操作符提前返回；正常转换后，再使用 `PositiveNonzeroInteger::new(x).map_err(ParsePosNonzeroError::from_creation)` 处理正常的结果。
