# <center>if</center>
## if 表达式
```rust
if condition {
}
```
condition 只能是 bool 类型。
## else if 处理多分支
```rust
if condition1 {
    ...
} else if condition2 {
    ...
}
```
## 配合 let 使用
```rust
let number = if condition { 5 } else { 6 };
```
