# trait 高级特性
## 在Trait定义中使用关联类型指定占位符类型
关联类型将一个类型占位符与一个trait连接起来，这样trait方法定义就可以在它们的签名中使用这些占位符类型。trait的实现者将指定要使用的具体类型，而不是特定实现的占位符类型。这样，我们就可以定义一个使用某些类型的特征，而不需要在实现特征之前确切地知道这些类型是什么。
```rust
pub trait Iterator {
    type Item;

    fn next(&mut self) -> Option<Self::Item>;
}
```
