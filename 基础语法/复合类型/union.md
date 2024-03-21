# union
union 类型内部的所有成员变量共享空间。

## union 特性

+ union的所有字段共享同一段存储；
+ 对 union 类型的成员变量无论读写，都只能在 unsafe 上下文中进行；
+ union 类型的成员的类型只能是以下几种（下述约束保证了成员是不需要析构的，也因此这些写操作不必放在 unsafe 块中）：
    + 满足 Copy trait 的类型；
    + &T 或者 &mut T 类型；
    + ManuallyDrop 类型；
    + 由以上类型组成的元组或者数组类型；
+ union 类型不能实现 Drop trait；

## union 基本操作
### 配合 match 使用
```rust
unsafe {
    match u {
        MyUnion {f1: 10} => { assert_eq!(10, u.f1); }
        MyUnion {f2} => { println!("{}", f2); }
    }
}
```
union 字段上模式匹配只能一次指定一个字段。

### union 所有权
由于union字段共享存储，因此拥有对union一个字段的写访问权就同时拥有了对其所有其他字段的写访问权。
```rust
union MyUnion { f1: u32, f2: f32 }

let mut u = MyUnion { f1: 1 };
    unsafe {
        let b1 = &mut u.f1;
        // 错误: 不能同时对 u (通过 u.f2)拥有多余一次的可变借用
        let b2 = &mut u.f2;

        *b1 = 5;
        // ^^^^首次借用在这里结束
    }
```
