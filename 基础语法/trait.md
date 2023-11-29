## 作为函数参数
在函数泛型种，我们可以限定泛型实现指定的trait，例如：
```rust
fn parse_csv_document<R: std::io::BufRead>(src: R) {
    ......
}
```
R限定为任何实现BufRead的类型，上面的代码可以改写成：
```rust
fn parse_csv_document(src: impl std::io::BufRead) {
    ......
}
```

## 作为返回类型
通过 -> impl MyTrait, 可以让函数返回 实现了MyTrait的类型
```rust
fn combine_vecs(v: Vec<i32>, u: Vec<i32>) -> impl Iterator<Item=i32> {
    ......
}
```
此外，还可以返回闭包
```riust
fn make_adder_function(y: i32) -> impl Fn(i32) -> i32 {
    let closure = move |x: i32| { x + y };
    closure
}
```
