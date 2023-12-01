# build-std
该特性允许你按照自己的需要重编译 core 等标准crate，而不需要使用Rust安装程序内置的预编译版本。
```
# .cargo/config.toml

[unstable]
build-std = ["core", "compiler_builtins"]
build-std-features = ["compiler-builtins-mem"]
```
通过 build-std-features 配置项设置为 ["compiler-builtins-mem"] 来启动 compiler_builtins 的特性。

# build
+ taget
