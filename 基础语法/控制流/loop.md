# <center> loop 使用指导</center>

## 基本语法
```rust
loop {
    ......
}
```

## loop 返回值
```rust
let mut count = 1;
let mut sum = 0;
let sum1to100 = loop {
    if count > 100 {
        sum += count;
        break sum;
    }
    count += 1;
};
```
## loop 多层嵌套
