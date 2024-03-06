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
```rust
loop {
    loop {
        if condtion {
            break;
        }
    }
}
```
当 loop 有多层嵌套，break 和 continue 只会引用于最内层的loop。通过 loop 标签，我们指定break 和 continue 的 loop。
```rust
'loop1': loop {
    loop {
        if condition {
            break 'loop1';
        }
    }
}


```
