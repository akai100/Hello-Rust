# build-std
该特性允许你按照自己的需要重编译 core 等标准crate，而不需要使用Rust安装程序内置的预编译版本。
```
# .cargo/config.toml

[unstable]
build-std = ["core", "compiler_builtins"]
```
