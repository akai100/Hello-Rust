## 实现从零开始实现 #![no_std]
### 1、创建项目
```shell
  entry point must be defined
```
此时文件内容如下：
```toml
//  Cargo.toml
[package]
name = "prj_no_std"
version = "0.1.0"
edition = "2021"

# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies]
```
```rust
// src/main.rs
fn main() {
    println!("Hello, world!");
}
```
### 2、 添加 #![no_std] 属性
```rust
// src/main.rs
#![no_std]

fn main() {
    println!("Hello, world!");
}
```
此时运行，报错如下：
```shell
error: cannot find macro `println` in this scope
 --> src\main.rs:3:5
  |
3 |     println!("Hello, world!");
  |     ^^^^^^^

error: `#[panic_handler]` function required, but not found

error: language item required, but not found: `eh_personality`
  |
  = note: this can occur when a binary crate with `#![no_std]` is compiled for a target where `eh_personality` is defined in the standard library
  = help: you may be able to compile for a target that doesn't need `eh_personality`, specify a target with `--target` or in `.cargo/config`

error: could not compile `prj_no_std` (bin "prj_no_std") due to 3 previous errors
```
+ 报错1：cannot find macro `println` in this scope
  println 由 std 库实现，我们无法再使用该宏，删除即可。
+ 报错2：`#[panic_handler]` function required, but not found
  编译器提示我们缺少一个 #[panic_handler] 函数，#[panic_handler] 标注了一个函数，该函数会在一个 panic 发生时调用，std 库默认会提供一个，现在需要我们自己实现：
  ```rust
  use core::panic::PanicInfo;

  /// 这个函数将在 panic 时被调用
  #[panic_handler]
  fn panic(_info: &PanicInfo) -> ! {
      loop {}
  }
  ```
  + 报错3： language item required, but not found: `eh_personality`
    语言项是一些编译器需求的特殊函数或类型。eh_personality 语言项标记的函数，将被用于实现栈展开（stack unwinding）。在其它一些情况下，栈展开并不是迫切需求的功能；
    因此，Rust 提供了在 panic 时中止（abort on panic）的选项。
    ```toml
    // Cargo.toml
    
    [profile.dev]
    panic = "abort"

    [profile.release]
    panic = "abort"
    ```
  + 报错4： error: requires `start` lang_item
    在加上上面的代码之后，构建又报上面的错，这里，我们的程序遗失了 start 语言项，它将定义一个程序的入口点。需要重写入口点：
    ```rust
    #[no_mangle]
    pub extern "C" fn _start() -> ! {
        loop {}
    }
    ```
    notice:
    我们通常会认为，当运行一个程序时，首先被调用的是 main 函数。但是，大多数语言都拥有一个运行时系统（runtime system），
    它通常为垃圾回收（garbage collection）或绿色线程（software threads，或 green threads）服务。

    在一个典型的使用标准库的 Rust 程序中，程序运行是从一个名为 crt0 的运行时库开始的。crt0 意为 C runtime zero，
    它能建立一个适合运行 C 语言程序的环境，这包含了栈的创建和可执行程序参数的传入。在这之后，这个运行时库会调用 Rust 的运行时入口点，
    这个入口点被称作 start语言项（“start” language item）。Rust 只拥有一个极小的运行时，它被设计为拥有较少的功能，如爆栈检测和打印栈轨迹（stack trace）。
    这之后，这个运行时将会调用 main 函数。
  + 报错5：note: LINK : fatal error LNK1561: entry point must be defined
    Windows 环境可能报上面的错，请看这篇博客：https://zhuanlan.zhihu.com/p/69393545
    在文件中的配置解决方案：
    ```toml
    // .cargo/toml
    [target.'cfg(target_env="msvc")']
    rustflags = [
        "-C", "link-arg=/entry:_start"
    ]
    ```
  + 报错6：fatal error LNK1221: a subsystem can't be inferred and must be defined
    ```rust
    // src/main.rs
    
    #![windows_subsystem = "windows"]
    ```
## 测试
cargo test 框架依赖std。如果需要支持测试，请看 测试目录下的。
