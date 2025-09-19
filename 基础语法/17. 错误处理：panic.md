## Rust 错误处理介绍
Rust 将错误分成两大类，**可恢复的** 和 **不可恢复的**。使用 Result<T, E> 处理可恢复的错误，panic! 宏 处理不可恢复的错误。

## panic
程序panic 会打印一个错误信息。展开并清理数据，然后退出。程序panic有两种方式：
+ 执行会造成程序panic的操作，比如访问超过数组结尾的内容
+ 显示调用 panic! 宏

程序 panic时的栈展开 或 终止
当出现panic，程序默认会开始 展开，Rust会回溯栈并清理它遇到的每一个函数的数据。另一个选择是直接终止，这个会不清理数据就会退出程序。通过在Cargo.toml 增加下面配置：
```toml
[profile.release]
panic = 'abort'
```

主动触发panic:
```rust
fn main() {
    panic!("crash and burn");
}
```
