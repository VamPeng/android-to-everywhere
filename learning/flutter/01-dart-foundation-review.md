---
type: review
area: Flutter
module: 01
status: completed
updated: 2026-09-01
---

# Flutter 01：Dart 核心基础快速复习

> 目标：快速恢复 Dart 业务代码阅读与编写能力。范围对应 `learning/flutter/01-dart-foundation.md` 的 9 个教学节点。

## 0. 一页总览

| 节点 | 必须记住的一句话 |
|---|---|
| 01.1 变量与常量 | `var` 推断类型；`final` 运行时只赋值一次；`const` 必须是编译时常量。 |
| 01.2 空安全 | `T` 不可空，`T?` 可空；优先安全处理，只有能证明非空时才用 `!`。 |
| 01.3 函数参数 | `{}` 是命名参数，`[]` 是可选位置参数；命名参数默认可选，可用 `required` 强制传入。 |
| 01.4 面向对象 | Dart 没有单独的 `interface` 关键字；任意类都隐式定义接口。 |
| 01.5 泛型/扩展/Mixin | 泛型约束类型；extension 补充调用形式；mixin 复用行为但不表达“是什么”。 |
| 01.6 集合 | `List` 有序可重复，`Set` 去重，`Map` 保存键值对；转换常用 `map/where/toList`。 |
| 01.7 Future | `Future<T>` 表示未来一次结果；`async/await` 不等于新线程，默认仍在当前 isolate。 |
| 01.8 Stream | `Stream<T>` 表示一段时间内的多个数据/错误/完成事件；`listen()` 返回可取消的订阅。 |
| 01.9 isolate | isolate 是独立内存和事件循环的并发单元；CPU 重任务才考虑移出主 isolate。 |

---

## 01.1 变量、类型、`final`、`const`

```dart
var name = 'Yuhui';       // 推断为 String，之后不能赋 int
Object value = 'text';    // 静态类型 Object，使用前通常要判断/转换
dynamic data = 'text';    // 跳过静态检查，错误可能推迟到运行时

final now = DateTime.now();       // 运行时确定，只能赋值一次
const maxRetry = 3;               // 编译时确定
const timeout = Duration(seconds: 3);
```

### `final` 与 `const`

| 对比 | `final` | `const` |
|---|---|---|
| 赋值次数 | 一次 | 一次 |
| 值确定时机 | 运行时也可以 | 必须编译时 |
| 引用对象 | 对象内部仍可能可变 | 整个对象图必须满足常量要求 |
| 示例 | `final time = DateTime.now()` | `const count = 3` |

局部 `const` 仍是局部变量，只在当前词法作用域可见；多个函数可定义同名常量，彼此无关。相同常量对象可能被 canonicalization 复用，但不要把它当作业务身份判断依据。

---

## 01.2 空安全

```dart
String name = 'A';       // 不可为 null
String? nickname;        // 可以为 null

final length = nickname?.length;       // nickname 为 null → null
final shown = nickname ?? '未设置';     // null 时使用默认值
final forced = nickname!.length;       // null 时运行期抛异常

late String token;       // 承诺稍后、使用前一定初始化
```

记忆顺序：

1. 能用不可空类型就不用 `?`。
2. 可空值优先用判断、`?.`、`??`。
3. `!` 不是判空，而是开发者向编译器担保。
4. `late` 不是默认值；未初始化就读取会抛 `LateInitializationError`。

```dart
if (nickname != null) {
  print(nickname.length); // 类型提升为 String
}
```

---

## 01.3 函数与参数

```dart
// 命名参数
String greet({required String name, String prefix = 'Hello'}) {
  return '$prefix, $name';
}

greet(name: 'Yuhui');

// 可选位置参数
String label(String name, [int? age]) {
  return age == null ? name : '$name ($age)';
}
```

| 写法 | 含义 |
|---|---|
| `String name` | 必传位置参数 |
| `[String? name]` | 可选位置参数 |
| `{String? name}` | 可选命名参数 |
| `{required String name}` | 必传命名参数 |
| `{String name = 'A'}` | 带默认值的命名参数 |

Dart 函数是一等对象：可以保存到变量、作为参数传入或作为返回值。

```dart
int calculate(int a, int b, int Function(int, int) operation) {
  return operation(a, b);
}

final result = calculate(2, 3, (a, b) => a + b);
```

---

## 01.4 类、构造函数、继承与接口

```dart
class User {
  final String id;
  final String name;

  const User({required this.id, required this.name});

  User.guest() : id = '0', name = 'Guest'; // 命名构造

  factory User.fromJson(Map<String, dynamic> json) {
    return User(
      id: json['id'] as String,
      name: json['name'] as String,
    );
  }
}
```

### 构造函数区别

- 普通/命名构造函数：负责初始化当前类的新实例。
- `factory`：不保证创建新实例，可以返回缓存对象、子类对象，且不能直接访问 `this`。

```dart
abstract class Repository {
  Future<User> getUser();
}

class ApiRepository implements Repository {
  @override
  Future<User> getUser() async => const User(id: '1', name: 'A');
}
```

| Dart | 语义 |
|---|---|
| `extends` | 继承实现；单继承 |
| `implements` | 只承诺接口，必须重新实现接口成员 |
| `abstract class` | 可包含抽象成员和已有实现 |
| `with` | 混入可复用行为 |

---

## 01.5 泛型、Extension、Mixin

### 泛型

```dart
class Result<T> {
  final T? data;
  final Object? error;

  const Result.success(this.data) : error = null;
  const Result.failure(this.error) : data = null;
}

T first<T>(List<T> items) => items.first;
```

泛型的作用：让容器或逻辑复用，同时保留编译期类型检查。

### Extension

```dart
extension StringValidation on String {
  bool get isValidPassword => length >= 8;
}

final valid = '12345678'.isValidPassword;
```

Extension 是静态解析的语法扩展，不是真的给原类增加成员，也不能保存实例状态。

### Mixin

```dart
mixin Logger {
  void log(String message) => print(message);
}

class UserService with Logger {}
```

适合复用横切行为；若要表达稳定的类型层级或业务契约，使用 `extends` / `implements`。

---

## 01.6 集合与转换

```dart
final list = <int>[1, 2, 2];
final set = <int>{1, 2, 2};          // {1, 2}
final map = <String, int>{'A': 1};

final result = list
    .where((value) => value.isEven)
    .map((value) => value * 10)
    .toList();                       // [20, 20]
```

关键点：

- `map()`、`where()` 通常返回惰性的 `Iterable`，需要列表时调用 `toList()`。
- `final list = [...]` 只禁止变量重新赋值，仍可 `list.add()`。
- 不可变集合可用 `List.unmodifiable(source)`。
- 展开：`[...a, ...b]`；可空展开：`[...?items]`。
- 条件元素：`[if (loggedIn) profile]`。

---

## 01.7 `Future`、`async/await` 与异常

```dart
Future<User> loadUser() async {
  try {
    final json = await requestUser();
    return User.fromJson(json);
  } catch (error, stackTrace) {
    print('$error\n$stackTrace');
    rethrow; // 保留原异常与调用链
  }
}
```

### 必须分清

- `Future<T>`：未来完成一次，结果是成功值或异常。
- `async`：函数立即返回 `Future`；函数体会执行到第一个真正挂起的 `await`。
- `await`：当前 async 函数暂停，不阻塞 isolate 的事件循环。
- `async/await` 默认不会创建新线程或新 isolate。
- CPU 密集循环即使放进 `async`，仍会阻塞主 isolate。

```dart
// 错误：没有 await，catch 捕获不到 Future 稍后产生的异常
try {
  loadUser();
} catch (_) {}

// 正确
try {
  await loadUser();
} catch (_) {}
```

并发等待：

```dart
final results = await Future.wait([
  loadProfile(),
  loadSettings(),
]);
```

---

## 01.8 `Stream`、订阅、取消与错误

```dart
Stream<int> counter() async* {
  yield 1;
  await Future<void>.delayed(const Duration(seconds: 1));
  yield 2;
}

final subscription = counter().listen(
  (value) => print(value),
  onError: (Object error, StackTrace stack) => print(error),
  onDone: () => print('done'),
  cancelOnError: false,
);

// 在真实生命周期结束或业务不再需要数据时取消
await subscription.cancel();
```

### Future vs Stream

| | `Future<T>` | `Stream<T>` |
|---|---|---|
| 结果数量 | 一次 | 0～多次 |
| 消费方式 | `await` / `then` | `listen` / `await for` |
| 生命周期 | 完成即结束 | 数据、错误、完成事件持续出现 |
| 取消 | Future 本身通常不能直接取消 | 取消 `StreamSubscription` |

### 单订阅与广播

- 单订阅 Stream：通常只能监听一次，适合文件读取、请求过程等有顺序的数据源。
- 广播 Stream：允许多个监听者，适合 UI 事件或共享通知。
- `asBroadcastStream()` 能改变监听形式，但不自动解决业务层的缓存、重放和生命周期问题。

### 取消语义

`cancel()` 表示订阅者不再接收后续事件。取消时机由真实生命周期决定，例如页面销毁、任务切换、请求废弃；不要为了演示而在 `listen()` 后立刻取消。

---

## 01.9 isolate 与主 isolate 阻塞

```dart
final result = await Isolate.run(() {
  return heavyCalculate();
});
```

### 核心模型

- 每个 isolate 有独立内存、事件循环和消息队列。
- isolate 之间不共享普通对象，通过消息传递通信。
- `Isolate.run()` 创建/使用一个隔离执行单元完成一次任务，并把结果传回。
- isolate 是 Dart 并发隔离模型，不应简单等同于 Java `Thread`。
- Dart VM 负责底层线程调度；业务代码通常控制 isolate/消息，而不是像 Java 那样直接操作某个线程对象。

### 什么时候使用

| 工作 | 选择 |
|---|---|
| 网络、数据库、文件等异步 I/O | `Future` / `async-await` |
| 连续异步事件 | `Stream` |
| 大 JSON 解析、图片处理、密集计算 | `Isolate.run()` 或长期 worker isolate |
| 高频短任务 | 避免每次都新建 isolate，考虑复用 worker |

判断标准：任务是否长时间占用 CPU，导致主 isolate 无法及时处理帧、输入和事件。

---

## Kotlin ↔ Dart 关键语义差异

| Kotlin | Dart | 注意 |
|---|---|---|
| `val` | `final` | 都禁止重新赋值，但不保证对象内部不可变。 |
| `const val` | `const` | 都要求编译期常量，但具体允许的类型和作用域规则不同。 |
| `Any` | `Object` | Dart 的 `Object` 不包含 `null`；要表示可空对象用 `Object?`。 |
| `Any?` | `Object?` | 都可包含 `null`。 |
| `!!` | `!` | 都是在运行时承担空值崩溃风险。 |
| 默认参数/命名调用 | 命名参数 `{}` | Dart 用 `required` 表示命名参数必传。 |
| `interface` | `implements` 任意类接口 | Dart 类会隐式定义接口。 |
| extension function | extension | 都是静态扩展，不是真正修改原类。 |
| coroutine `suspend` | `Future` + `async/await` | 都能挂起异步流程，但运行时模型与结构化并发能力不同。 |
| `Flow` | `Stream` | 都表示异步序列，但冷/热、取消和操作符语义不能直接一一类比。 |
| `Thread` / Dispatcher | isolate | isolate 内存隔离，不是公开线程对象的替代语法。 |

---

## 高频错误清单

- 把 `dynamic` 当成 Kotlin `Any?`：`dynamic` 会绕过大量静态检查。
- 认为 `final List` 不可修改：它只是不能换引用。
- 用 `!` 代替空值建模：可能把编译期问题推迟为运行时崩溃。
- 认为 `async` 自动切后台线程：CPU 重任务仍可能卡 UI。
- 调用异步函数却遗漏 `await`：执行顺序和异常捕获都会改变。
- `listen()` 后马上 `cancel()`：很可能一个异步事件都收不到。
- 重复监听单订阅 Stream：会产生状态错误。
- 将 isolate 等同线程并试图共享对象：isolate 以隔离和消息传递为核心。

---

## 5 分钟自测

先口答，再看答案。

1. `final` 和 `const` 的决定性区别是什么？
2. `String?`、`?.`、`??`、`!` 分别表示什么？
3. `{required String id}` 为什么既是命名参数又是必传参数？
4. `factory` 构造函数为什么可能不创建新对象？
5. `implements` 与 `extends` 的实现复用差异是什么？
6. 为什么 `list.map(...).where(...)` 的结果通常不是 `List`？
7. `await` 会不会阻塞主 isolate？CPU 循环放入 `async` 呢？
8. Stream 的错误是不是一定意味着 Stream 立刻结束？
9. `subscription.cancel()` 取消的是什么？
10. isolate 为什么不能直接等同 Java Thread？

### 答案

1. `final` 可在运行时确定；`const` 必须在编译时确定。
2. 可空类型、安全访问、空值默认值、非空断言。
3. `{}` 定义命名参数；`required` 再约束调用方必须传入。
4. `factory` 可以返回缓存实例或其他实现类实例。
5. `extends` 继承实现；`implements` 只继承接口契约，成员需要重新实现。
6. `map/where` 返回惰性 `Iterable`，调用 `toList()` 才得到列表。
7. `await` 挂起当前 async 函数，不阻塞事件循环；CPU 循环仍会阻塞所在 isolate。
8. 不一定；是否继续取决于数据源以及监听方式，例如 `cancelOnError`。
9. 取消当前监听关系，后续事件不再交付给该订阅者。
10. isolate 拥有独立内存和事件循环，以消息通信；底层线程由运行时调度。

---

## 结业判断

如果你能不看答案解释下面这条完整链路，Flutter 01 的核心知识就已恢复：

```text
Map<String, dynamic>
→ factory UserDto.fromJson
→ Repository 返回 Future<Result<User>>
→ async/await 捕获异常
→ Stream 上报多次进度
→ 页面生命周期结束时取消 StreamSubscription
→ CPU 密集转换才移入 isolate
```
