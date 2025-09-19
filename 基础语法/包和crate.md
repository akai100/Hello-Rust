+ **包和crate介绍**
Rust有两个不同的术语与模块系统有关：包装箱（crate）和模块（module）。
    + crate
  
    crate是 Rust 在编译时最小的代码单位。crate 可以包含模块，模块可以定义在其他文件，然后和 crate 一起编译。
crate 有两种形式：二进制项和库。二进制项 可以被编译为可执行程序。
库 并没有 main 函数，它们也不会编译为可执行程序，它们提供一些诸如函数之类的东西，使其他项目也能使用这些东西。
crate root 是一个源文件，Rust 编译器以它为起始点，并构成你的 crate 的根模块
    + 包
  
    包（package）是提供一系列功能的一个或者多个 crate。一个包会包含一个 Cargo.toml 文件，阐述如何去构建这些 crate。Cargo 就是一个包含构建你代码的二进制项的包。Cargo 也包含这些二进制项所依赖的库。
    包中可以包含至多一个库 crate(library crate)。包中可以包含任意多个二进制 crate(binary crate)，但是必须至少包含一个 crate（无论是库的还是二进制的）。

+ **包装箱（crate)**
每个包装箱有一个隐含的根模块包含模块的代码。 我们用cargo 创建一个新包装箱：
```rust
cargo new phrases
```
新生成的目录结构：

![99b3c56dacafe86d918983411d9f8e55.png](:/8ed1a9732f754655b1d24565db39f0f8)

src/lib.rs 是我们包装箱的根。

我们可以在lib.rs来定义模块，例如：
```rust
mod english {
    mod greetings {
    }
    
    mod farewells {
    }
}

mod japanese {
    mod greetings {
    }
    
    mod farewells {
    }
}
```

在mod中，我们可以定义子 mod。因为这个包装箱的根文件叫做lib.rs，且没有一个main函数。cargo 会把这个包装箱构建为一个库。
