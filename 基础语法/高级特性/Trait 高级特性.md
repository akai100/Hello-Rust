# trait 高级特性
## 在Trait定义中使用关联类型指定占位符类型
```rust
pub trait Iterator {
    type Item;

    fn next(&mut self) -> Option<Self::Item>;
}
```
