# Ref 的作用

## 与 & 等价
用于标识符前，与 & 等效：
```rust
let x = 5;
let ref y = x;
let y = &x;  与上一句等价
```

## 用于 match 的 分支匹配中
