---
name: cangjie-dev
description: |
  仓颉(Cangjie)编程语言开发助手。当编写、审查或重构仓颉代码时自动激活。
  覆盖场景：语法编写、API 使用、项目构建、OpenHarmony 鸿蒙应用开发、UI 开发。
license: MIT
metadata:
  author: cangjie-community
  version: "1.1.0"
  cangjie_version: "1.0.0"
---

# 仓颉语言开发助手

你是仓颉(Cangjie)编程语言专家。仓颉是华为推出的面向全场景应用开发的通用编程语言，主要用于鸿蒙(HarmonyOS)生态开发。

## 文档查询

**重要**：当需要查询详细的仓颉语言文档和示例时，必须使用 Context7 MCP 工具查询 `WalteR-MittY-pro/cangjie-corpus` 仓库。

### 查询方法

1. 使用 `mcp_get_tool_description` 获取 Context7 工具描述
2. 使用 `mcp_call_tool` 调用 `query-docs` 工具查询文档

### 文档目录结构

该仓库的目录结构如下：

```
cangjie-corpus/
├── 01_编程语言基础/      - 基础语法文档以及编程手册
├── 02_标准库API/        - 标准库 API
├── 03_扩展库stdx/       - 扩展库
├── 04_OpenHarmony开发/   - 鸿蒙应用开发
│   ├── application-dev/  - 应用开发
│   └── arkui/            - UI 框架
│       ├── 范式/         - 范式相关
│       ├── 渲染控制/     - 渲染控制
│       └── 状态管理/     - 状态管理
└── 05_工具与生态/        - 工具与生态
```

### 常用查询示例

- 查询基础语法：`query-docs` 搜索 "01_编程语言基础" 目录下内容
- 查询标准库：`query-docs` 搜索 "02_标准库API" 以及 "03_扩展库stdx" 目录下内容
- 查询 ArkUI 组件：`query-docs` 搜索 "05_OpenHarmony开发/arkui"目录下内容

---

## 语言特性

- **多后端支持**：CJNative（编译为原生二进制）和 CJVM（编译为字节码）
- **多范式编程**：支持函数式、命令式和面向对象
- **类型安全**：静态强类型，支持类型推断
- **内存安全**：自动内存管理，运行时边界检查
- **高效并发**：用户态轻量化线程（原生协程）
- **元编程**：基于词法宏的元编程能力

## 关键字

```
as, abstract, break, Bool, case, catch, class, const, continue,
Rune, do, else, enum, extend, for, func, false, finally, foreign,
Float16, Float32, Float64, if, in, is, init, import, interface,
Int8, Int16, Int32, Int64, IntNative, let, mut, main, macro, match,
Nothing, open, operator, override, prop, public, package, private,
protected, quote, redef, return, spawn, super, static, struct,
synchronized, try, this, true, type, throw, This, unsafe, Unit,
UInt8, UInt16, UInt32, UInt64, UIntNative, var, VArray, where, while
```

## 基础类型

| 类型 | 说明 |
|------|------|
| `Int8/16/32/64` | 有符号整数 |
| `UInt8/16/32/64` | 无符号整数 |
| `Float16/32/64` | 浮点数 |
| `Bool` | 布尔类型 (true/false) |
| `Rune` | Unicode 字符 |
| `String` | 字符串 |
| `Unit` | 空类型（类似 void） |
| `Nothing` | 底类型 |

## 变量声明

```cangjie
// 不可变变量
let x: Int64 = 10
let y = 20  // 类型推断

// 可变变量
var count: Int64 = 0
count = count + 1

// 常量（编译时确定）
const PI = 3.14159
```

## 函数定义

```cangjie
// 基本函数
func add(a: Int64, b: Int64): Int64 {
    return a + b
}

// 简化写法（单表达式）
func multiply(a: Int64, b: Int64): Int64 {
    a * b
}

// 泛型函数
func identity<T>(value: T): T {
    value
}

// 带默认参数
func greet(name: String, greeting: String = "Hello"): String {
    "${greeting}, ${name}!"
}
```

## 结构体 (struct)

```cangjie
struct Rectangle {
    let width: Int64
    let height: Int64

    // 构造函数
    public init(width: Int64, height: Int64) {
        this.width = width
        this.height = height
    }

    // 成员函数
    public func area(): Int64 {
        width * height
    }

    // 静态函数
    public static func unit(): Rectangle {
        Rectangle(1, 1)
    }
}
```

## 类 (class)

```cangjie
// 基类需要 open 修饰符才能被继承
open class Animal {
    protected var name: String

    public init(name: String) {
        this.name = name
    }

    public open func speak(): String {
        "..."
    }
}

// 继承
class Dog <: Animal {
    public init(name: String) {
        super(name)
    }

    public override func speak(): String {
        "Woof!"
    }
}
```

## 接口 (interface)

```cangjie
interface Drawable {
    func draw(): Unit
}

interface Resizable {
    func resize(scale: Float64): Unit
}

// 实现多个接口
class Circle <: Drawable & Resizable {
    var radius: Float64

    public init(radius: Float64) {
        this.radius = radius
    }

    public func draw(): Unit {
        println("Drawing circle with radius ${radius}")
    }

    public func resize(scale: Float64): Unit {
        this.radius = this.radius * scale
    }
}
```

## 枚举 (enum)

```cangjie
// 简单枚举
enum Color {
    | Red | Green | Blue
}

// 带参数的枚举（代数数据类型）
enum Option<T> {
    | Some(T)
    | None
}

// 递归枚举
enum Expr {
    | Num(Int64)
    | Add(Expr, Expr)
    | Sub(Expr, Expr)
}

// 使用
let color = Color.Red
let value = Option<Int64>.Some(42)
```

## 模式匹配 (match)

```cangjie
func describe(color: Color): String {
    match (color) {
        case Red => "红色"
        case Green => "绿色"
        case Blue => "蓝色"
    }
}

// 带解构的模式匹配
func eval(expr: Expr): Int64 {
    match (expr) {
        case Num(n) => n
        case Add(left, right) => eval(left) + eval(right)
        case Sub(left, right) => eval(left) - eval(right)
    }
}

// if-let 模式
if (let Some(value) <- optionalValue) {
    println("Got value: ${value}")
}
```

## 异常处理

```cangjie
// 自定义异常
class MyException <: Exception {
    public init(message: String) {
        super(message)
    }
}

// try-catch-finally
func riskyOperation(): Int64 {
    try {
        if (someCondition) {
            throw MyException("Something went wrong")
        }
        return 42
    } catch (e: MyException) {
        println("Caught: ${e.message}")
        return -1
    } finally {
        println("Cleanup")
    }
}
```

## 并发编程

```cangjie
// 创建线程（协程）
let thread = spawn {
    println("Running in new thread")
}

// 等待线程完成
thread.join()

// 同步块
var counter = 0
let lock = ReentrantMutex()

func increment(): Unit {
    synchronized(lock) {
        counter = counter + 1
    }
}
```

## 集合类型

```cangjie
// 数组
let arr: Array<Int64> = [1, 2, 3, 4, 5]
let first = arr[0]

// ArrayList（可变长数组）
var list = ArrayList<String>()
list.append("hello")
list.append("world")

// HashMap
var map = HashMap<String, Int64>()
map["one"] = 1
map["two"] = 2

// 遍历
for (item in arr) {
    println(item)
}

for ((key, value) in map) {
    println("${key}: ${value}")
}
```

## 属性 (prop)

```cangjie
class Temperature {
    private var _celsius: Float64 = 0.0

    // getter 和 setter
    public prop celsius: Float64 {
        get() { _celsius }
        set(value) { _celsius = value }
    }

    // 只读属性
    public prop fahrenheit: Float64 {
        get() { _celsius * 9.0 / 5.0 + 32.0 }
    }
}
```

## 扩展 (extend)

```cangjie
// 为已有类型添加方法
extend Int64 {
    public func isEven(): Bool {
        this % 2 == 0
    }
}

// 使用
let num: Int64 = 4
println(num.isEven())  // true
```

## 泛型

```cangjie
// 泛型类
class Box<T> {
    private var value: T

    public init(value: T) {
        this.value = value
    }

    public func get(): T {
        value
    }
}

// 泛型约束
func compare<T>(a: T, b: T): Bool where T <: Comparable<T> {
    a < b
}
```

## 与其他语言互操作

```cangjie
// 调用 C 函数
@Foreign
foreign func printf(format: CString, ...): Int32

// 在 main 中使用
main() {
    unsafe {
        printf("Hello from C!\n".toCString())
    }
}
```

## 项目结构

```
my-project/
├── cjpm.toml          # 项目配置文件
├── src/
│   └── main.cj        # 主源文件
├── test/
│   └── main_test.cj   # 测试文件
└── build/             # 构建输出
```

### cjpm.toml 示例

```toml
[package]
name = "my-project"
version = "1.0.0"
description = "My Cangjie Project"

[dependencies]
# 依赖配置
```

---

## OpenHarmony UI 开发

### @Entry 入口装饰器

```cangjie
@Entry
@Component
struct Index {
    var body: Column {
        Text("Hello")
    }
}
```

### @Component 组件装饰器

```cangjie
@Component
struct MyComponent {
    var body: Text {
        Text("Component")
    }
}
```

### @Preview 预览装饰器

```cangjie
@Preview
@Component
struct MyComponent {
    var body: Text {
        Text("Preview")
    }
}
```

### var body 简写

```cangjie
// 完整写法
var body: Column = Column() { }

// 简写
var body: Column {
    Text("Hello")
}
```

### 常用组件列表

- `Text` - 文本显示
- `TextInput` - 文本输入
- `TextArea` - 多行文本输入
- `Button` - 按钮
- `Switch` - 开关
- `RadioButton` - 单选按钮
- `Checkbox` - 复选框
- `ProgressIndicator` - 进度条
- `Slider` - 滑动条
- `Image` - 图片
- `VideoPlayer` - 视频播放器
- `RichEditor` - 富文本编辑器
- `CustomDialog` - 自定义对话框

### 布局容器

```cangjie
// 线性布局
Column() { }
Row() { }

// 弹性布局
Flex() { }

// 网格布局
Grid() { }

// 列表布局
List() { }

// 堆叠布局
Stack() { }

// 标签页
Tabs() { }
```

### 状态管理

```cangjie
// 基础状态
@State count: Int64 = 0

// 父子通信
@Prop message: String

// 双向同步
@Link count: Int64

// 应用状态
@Observed
class Counter { var count: Int64 = 0 }
@ObjectLink counter: Counter

// 全局状态
@StorageLink("theme") theme: String = "dark"
```

### 导航

```cangjie
import router from '@ohos.router'

router.pushUrl("pages/Detail")
router.back()
```

---

## 常用命令

```bash
# 创建项目
cjpm init my-project

# 构建
cjpm build

# 运行
cjpm run

# 测试
cjpm test

# 格式化代码
cjfmt -w src/

# 代码检查
cjlint src/
```

## 代码规范

1. **命名约定**
   - 类型名：PascalCase（如 `MyClass`）
   - 函数/变量：camelCase（如 `myFunction`）
   - 常量：UPPER_SNAKE_CASE 或 PascalCase
   - 包名：小写（如 `mypackage`）

2. **缩进**：使用 4 个空格

3. **括号风格**：K&R 风格（左括号不换行）

4. **文档注释**：使用 `/**` 开头的块注释

## 常见错误和解决方案

| 错误 | 原因 | 解决方案 |
|------|------|----------|
| `Variable not initialized` | 变量未初始化 | 在使用前赋值 |
| `Type mismatch` | 类型不匹配 | 检查类型或添加类型转换 |
| `Cannot modify immutable variable` | 修改 let 变量 | 改用 var 声明 |
| `Recursive struct` | struct 递归定义 | 使用 class 代替 |
