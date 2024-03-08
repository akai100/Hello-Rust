# trait 高级特性
## 在Trait定义中使用关联类型指定占位符类型
关联类型将一个类型占位符与一个trait连接起来，这样trait方法定义就可以在它们的签名中使用这些占位符类型。trait的实现者将指定要使用的具体类型，而不是特定实现的占位符类型。这样，我们就可以定义一个使用某些类型的特征，而不需要在实现特征之前确切地知道这些类型是什么。
```rust
pub trait Iterator {
    type Item;

    fn next(&mut self) -> Option<Self::Item>;
}
```
Item 是一个占位符，

## 默认泛型类型参数和运算符重载
```rust
trait Add<Rhs=Self> {
    type Output;

    fn add(self, rhs: Rhs) -> Self::Output;
}
```
## 消除歧义的完全限定语法：调用同名方法
rust 运行实现两个 trait，即使这两个 trait 有相同名称、相同参数的方法。
```rust
trait Pilot {
    fn fly(&self);
}

trait Wizard {
    fn fly(&self);
}

struct Human;

impl Pilot for Human {
    fn fly(&self) {
        println!("This is your captain speaking.");
    }
}

impl Wizard for Human {
    fn fly(&self) {
        println!("Up!");
    }
}

impl Human {
    fn fly(&self) {
        println!("*waving arms furiously*");
    }
}
```
我们在调用时，怎么指定调用那个函数:
```rust
fn main() {
    let person = Human;
    Pilot::fly(&person);
    Wizard::fly(&person);
    person.fly();
}
```
``` person.fly() ``` 默认调用为结构体定义的方法。
当实现两个或多个trait存在相同命名和参数的方法时，调用相关方法时，必须指定 trait。
