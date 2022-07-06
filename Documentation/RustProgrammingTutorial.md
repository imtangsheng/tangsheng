# Rust 教程

参考

[菜鸟教程](https://www.runoob.com/rust/rust-tutorial.html)

[Rust语言圣经(Rust Course)](https://course.rs/about-book.html)

## 目录
- [Rust关键字](#rust关键字)


## Rust关键字
函数、变量、参数、结构体字段、模块、包、常量、宏、静态值、属性、类型、特征或生命周期

### 关键字

关键字 | 说明
-|-
as | 强制类型转换，或use 和 extern crate包和模块引入语句中的重命名
break | 立刻退出循环
const | 定义常量或原生常量指针（constant raw pointer）
continue | 继续进入下一次循环迭代
crate | 链接外部包
dyn | 动态分发特征对象
else | 作为 if 和 if let 控制流结构的 fallback
enum | 定义一个枚举类型
extern | 链接一个外部包,或者一个宏变量(该变量定义在另外一个包中)
false | 布尔值 false
fn | 定义一个函数或 函数指针类型 (function pointer type)
for | 遍历一个迭代器或实现一个 trait 或者指定一个更高级的生命周期
if | 基于条件表达式的结果来执行相应的分支
impl | 为结构体或者特征实现具体功能
in | for 循环语法的一部分
let | 绑定一个变量
loop | 无条件循环
match | 模式匹配
mod | 定义一个模块
move | 使闭包获取其所捕获项的所有权
mut | 在引用、裸指针或模式绑定中使用，表明变量是可变的
pub | 表示结构体字段、impl 块或模块的公共可见性
ref | 通过引用绑定
return | 从函数中返回
Self | 实现特征类型的类型别名
self | 表示方法本身或当前模块
static | 表示全局变量或在整个程序执行期间保持其生命周期
struct | 定义一个结构体
super | 表示当前模块的父模块
trait | 定义一个特征
true | 布尔值 true
type | 定义一个类型别名或关联类型
unsafe | 表示不安全的代码、函数、特征或实现
use | 在当前代码范围内(模块或者花括号对)引入外部的包、模块等
where | 表示一个约束类型的从句
while | 基于一个表达式的结果判断是否继续循环


### 保留做将来使用的关键字
如下关键字没有任何功能，不过由 Rust 保留以备将来的应用。

保留字 | 无
-|-
abstract
async
await
become
box
do
final
macro
override
priv
try
typeof
unsized
virtual
yield


### 原生标识符

原生标识符（Raw identifiers）允许你使用通常不能使用的关键字，其带有 r# 前缀。