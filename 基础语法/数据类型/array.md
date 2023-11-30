# array（数组）
固定长度的数组，用 [T; N] 表示，T 表示数组元素类型，N 表示数组长度。N 必须是常量，对编译器是确定的。
## 创建数组
+ 包含元素的列表
  ```rust
  let arr = [1, 2, 3];
  ```
+ 重复表达式[expr; N], 其中 N 是 在数组中重复 expr 的此时， expr 必须是：
    + 实现 Copy trait 的类型的值
    + const 值
  ```rust
  let arr = [0; 3];
  ```
  notice: 其中  N 等于 0 是允许的，会创建一个空数组，expr的值也仍然会计算，并立即丢弃。
## 数组实现的 trait
### 对任意长度的数组
+ Copy
+ Clone
+ Debug
+ IntoIterator
+ PartialEq, ParitialOrd, Eq, Ord
+ Hash
+ AsRef
+ Borrow, BorrowMut
notice: 元素类型必须实现对应的trait
### 大小为 0 到 32 的数组
+ Default
  trait 实现是静态生成的，最大大小为32。
### 大小 1 到 12 的数组
+ From<Tuple>
## 类型转换
### 强转转换为 slices([T])
### 切片转换为 数组
切片具有动态大小，并且不强制转换为数组。使用slice.try_into() 或 <ArrayType>::try_form(slice).unwrap()

