# fn: 函数指针
函数指针是指向 code 的指针，而不是数据。他们可以像函数被调用。类似于引用，函数指针被假定为不为空。

## 普通函数指针
通过强制转换不能捕获环境的普通函数或闭包而捕获得。
```rust
fn add_one(x: usize) -> usize {
    x + 1
}

let ptr: fn(usize) -> usize = add_one;
assert_eq!(ptr(5), 6);

let clos: fn(usize) -> usize = |x| x + 5;
assert_eq!(clos(5), 10);
```
普通函数 fn() 函数指针只能指向安全函数， 可以通过 unfase fn() 函数指向不安全函数
```rust
unsafe fn add_one_unsafely(x: usize) -> usize {
    x + 1
}

let unsafe_ptr: unsafe fn(usize) -> usize = add_one_unsafely;  // 既可以指向不安全函数也可以指向安全函数
```
