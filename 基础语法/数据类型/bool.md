# bool 类型
bool 代表一个值，它只能是 true 或 false。 如果将 bool 转换为整数，则 true 将为 1，false 将为 0.

## 实现
+ pub fn then_some<T>(self, t: T) -> Option<T>
如果 bool 是 true, 则返回 Some(t), 否则返回 None。
+ pub fn then<T, F: FnOnce() -> T>(self, f: F) -> Option<T>
如果 bool 是 true，则返回 Some(f())，否则返回 None。
