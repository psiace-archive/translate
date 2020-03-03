---
title: Early Impressions of Go from a Rust Programmer
title-cn: 一位 Rust 程序员对 Go 的初步印象
author: ["Nick Cameron"]
translator: ["Chojan Shang(尚卓燃)", "Wucong(吴聪)"]
date: 2020-02-26
summary: Nick Cameron is a long-time Rust programmer who has recently started using Go. In this post, he talks about his early impressions of Go. Read this post to learn more.
summary-cn: Nick Cameron 是长期使用 Rust 的程序员，最近开始接触 Go。在这篇文章中，他谈论了他对 Go 的初步印象。阅读这篇文章以了解更多信息。
tags: ["Go", "Rust"]
categories: ["Engineering"]
image: /images/blog/early-impressions-of-go-from-a-rust-programmer.jpg
---

![Early impressions of Go from a Rust programmer](media/early-impressions-of-go-from-a-rust-programmer.jpg)

I've been using [Go](<https://en.wikipedia.org/wiki/Go_(programming_language)>) for the past few weeks. It's my first time using Go for a large (-ish), serious project. I've previously looked at Go a lot and played with examples and toy programs when researching features for [Rust](<https://en.wikipedia.org/wiki/Rust_(programming_language)>). Real programming is a very different experience.

过去几周，我一直在用 [Go](<https://en.wikipedia.org/wiki/Go_(programming_language)>) 语言编写程序。 这是我首次在大型且重要的项目中使用 Go。在研究 [Rust](<https://en.wikipedia.org/wiki/Rust_(programming_language)>) 的特性时，我也看了很多关于 Go 的内容，包括体验示例和编写玩具程序。但真正用它编程又是一种完全不同的体验。

I thought it would be interesting to write about my impressions. I'll try and avoid too much comparison with Rust, but since that is the language I'm coming from, there will be some. I should declare in advance a strong bias for Rust, but I'll do my best to be objective.

我觉得把这次体验写下来应该会很有趣。在这篇文章中，我会尽量避免将 Go 与 Rust 进行过多的比较，不过，由于我是从 Rust 转向 Go，难免也会包含一些比较。应该事先声明的是，我更偏袒 Rust ，但会尽力做到客观。

## General impression 总体印象

Programming with Go is nice. It had everything I wanted in the libraries and there were not too many rough edges. Learning it was a smooth experience, and it is a well-designed and practical language. Some examples: once you know the syntax, many idioms from other languages carry over to Go. Once you've learned some Go, it is relatively easy to predict other features. With some knowledge of other languages, I was able to read Go code and understand it without too much googling.

用 Go 编程的感觉很棒。库程序里有我想要的一切，总体实现较为完善。学习体验也十分顺畅，不得不说，Go 是一种经过精心设计的实用性语言。举个例子：一旦你知悉了 Go 的语法，就能将其他语言中惯用法延续到 Go 中。只要你学会一些 Go ，就可以相对轻易地推测 Go 语言的其他特性。凭借一些来自其他语言的知识，我能够阅读并理解 Go 代码，而不需要过多的搜索（Google）。

It is a lot less frustrating and a lot more productive than using C/C++, Java, Python, etc. It did feel, however, like part of that generation of languages. It has learnt some lessons from them, and I think it is probably the best language of that generation; but it is definitely part of that generation. It is an incremental improvement, rather than doing something radically different (to be clear, this is not a value judgement, incremental is often good in software engineering). A good example of this is `nil`: languages like Rust and Swift have removed the concept of `null` and eliminated a whole class of errors. Go makes it a bit less dangerous: no null _values_, distinguishes between `nil` and `0`. But the core idea is still there, and so is the common runtime error of dereferencing a null pointer.

与 C/C++、 Java、 Python 等相比，Go 并没有那么多痛点，而且更具生产力。然而，它还是与这些语言处在同一个时代。尽管它从其他语言身上吸取了一些教训，甚至我个人认为它可能是那一代语言中最好的那个，但绝对还属于那一代语言。这是一种渐进式的改进，而不是推陈出新（需要明确的是，这不是意味着对其价值的批判，从软件工程的角度，渐进式改进通常会带来好的影响）。一个很好的例证是 `nil`：像 Rust 和 Swift 这样的语言已经去除了 `null` 的概念，并且消除了相关的一整类错误。Go 降低了一部分风险：_没有空值_，在 `nil` 和 `0` 之间进行区分。但其核心思想仍未改变，同样还会出现解空指针引用这种常见的运行时错误。

## Learnability 易学性

Go is incredibly easy to learn. I know this is an often-touted benefit, but I was really surprised how quickly I was able to be productive. Thanks to the language, docs, and tools, I was writing 'interesting', commit-able code after literally two days.

Go 非常易学。我知道人们经常吹捧这一点，但是我真的为自己生产力的飞速提高而感到震惊。多亏了 Go 语言以及它的文档和工具，我仅仅花了两天时间就可以写出「有价值」、可以提交的代码。

A few factors contributing to learnability are:

有助于易学性的几个因素是：

- Go is small. Lots of languages try to be small, Go really is small; really small. (This is mostly a good thing and I'm impressed with the discipline this must have taken).
- The standard library is good (and again, small). Finding and using libraries from the ecosystem is very easy.
- There is very little in the language which is not in other languages. Go takes lots of bits from other established languages, polishes them, and puts them together nicely. It tries very hard to avoid novelty.

- Go 很精简。很多语言都试图让自己看起来小巧，但 Go 真正做到了这一点。（这基本上是一件好事，我对这种自律精神印象深刻）
- 标准库很出色（同样，也很小）。从生态系统中寻找并使用库程序非常容易。
- 几乎没有其他语言中所不具备的东西。Go 从其他既存语言中提取了很多内容，并进行完善，最后将它们很好地组合在一起。它在避免标新立异这一方面做了极大努力。

## Boilerplate 乏味的样板式代码

Go code becomes very repetitive very quickly. It is missing any mechanism like macros or generics for reducing repetition (interfaces are nice for abstraction, but don't work so well to reduce code duplication). I often end up with lots of functions, identical except for types.

Go 代码很快就会变得非常重复。这是由于它缺乏宏或者泛型这种用于减少重复的机制，（接口虽然有利于抽象，但在减少代码重复方面作用没有那么大)。最终我会写很多函数，而他们除了类型不同之外其他甚至完全一样。

Error handling also causes repetition. Many functions have more `if err != nil { return err }` boilerplate than interesting code.

错误处理也会导致重复。许多函数中像 `if err != nil { return err }` 这样的样板式代码甚至比那些真正有价值的代码还要多。

Using generics or macros to reduce boilerplate is sometimes criticised for making code easy to write at the expense of making it harder to read. But I found the opposite with Go. It is quick and easy to copy and paste code, but reading Go code is frustrating because you have to ignore so much of it or search for subtle differences.

使用泛型或宏来减少样板式代码有时会受到批评，理由是不应为使代码易于编写而使其丧失可读性。我发现 Go 恰恰提供了一个反例，复制和粘贴代码往往既快速又简单，阅读代码却会令人灰心丧气，因为你不得不忽略大量的无关代码或者在大量的相同代码中找到细微的不同。

## Things I like 我喜欢的东西

- Compile times. Definitely quick; definitely a lot quicker than Rust. But not actually as quick as I was expecting (it feels to me to be similar to or a little faster than C/C++ for medium to large projects, I was kind of expecting instant).
- Go routines and channels. Having lightweight syntax for spawning Go routines and using channels is really nice. It really shows the power of syntax that such a small detail makes concurrent programming feel so much nicer than in other languages.
- Interfaces. They're not very sophisticated but they are easy to understand and use, and useful in a lot of places.
- `if ...; ... { }` syntax. Being able to restrict the scope of variables to the body of `if` statements is nice. This has a similar effect to `if let` in Swift and Rust, but is more general purpose (Go does not have pattern matching like Swift and Rust, so it cannot use `if let`.
- Testing and doc comments are easy to use.
- The `Go` tool is nice - having everything in one place rather than requiring multiple tools on the command line.
- Having a garbage collector (GC)! Not thinking about memory management really does make programming easier.
- Varargs.

- 编译时间：绝对快，可以确定要比 Rust 快得多。但实际上，它并没有我预期的那么快（对于中型到大型项目，我感觉它的速度只是与 C/C++ 相接近，或者稍微快一点。而我更加期待能够即时编译。）
- 协程（goroutine）和信道（channel）：值得称赞的是，Go 为生成协程和使用信道提供了轻量级的语法。尽管只是一个小细节，却使 Go 的并发编程体验比其他语言更优越，它真正揭示了语法的力量。
- 接口：它们并不复杂，但是很容易理解和使用，并且在很多地方都很实用。
- `if ...; ... { }` 语法：可以将变量的作用域限制在 `if` 语句真的很好。这与 Swift 及 Rust 中的 `if let` 起着相似的效果，但用途更为广泛（Go 没有像 Swift 和 Rust 那样的模式匹配，所以它无法使用 `if let` 。）
- 测试和文档注释都很容易使用。
- `Go` 工具链非常友好 —— 将所有东西都放在一个地方，而不需要在命令行上使用多个工具。
- 拥有垃圾收集器（GC）！不用考虑内存管理真的会使编程更加轻松。
- 可变参数。

## Things I did not like 我不喜欢的东西

In no particular order.

以下内容没有特定的顺序。

- `nil` slices - `nil`, a `nil` slice, and an empty slice are all different. I'm pretty sure you only need two of those things, not three.
- No first class enums. Using constants feels backwards.
- Disallowing import cycles. This really limits how useful packages are for modularising a project, since it encourages putting lots of files in a package (or having lots of small packages, which can be just as bad if files which should be together are not).
- `switch` may be non-exhaustive.
- `for ... range` returns a pair of index/value. Getting just the index is easy (just ignore the value) but getting just the value requires being explicit. This seems back-to-front to me since I need the value and not the index in most cases.
- Syntax:
  - Inconsistency between definitions and uses.
  - Pickiness of the compiler (e.g., requiring or forbidding trailing commas); this is mostly alleviated by good tooling, but there a still a few times when this creates an annoying extra step.
  - When using multiple-value return types, parentheses are required on the type, but not in the `return` statement.
  - Declaring a struct requires two keywords (`type` and `struct`).
  - Using capitalisation for marking variables public or private. It's like Hungarian notation but worse.
- Implicit interfaces. I know I have this on my thing I like list too, but sometimes it is really annoying - e.g., trying to find all types which implement an interface, or which interfaces are implemented for a given type.
- You can't write functions with a receiver in a different package, so even though interfaces are 'duck typed' they can't be implemented for upstream types making them much less useful.

- `nil` 切片：要知道 `nil`、`nil` 切片和空切片三者都不相同，我敢保证我们只需要其中的两个，而不需要第三个。
- 枚举类型并不是第一公民：使用常量模拟枚举让人感觉是一种倒退。
- 不允许循环引用：这实际上限制了包在划分项目模块中的可用性，因为它变相鼓励了在一个包中堆积大量文件（或拥有大量零碎的小包，如果本该放在一起的文件四处分散，这也同样糟糕）。
- `switch` 允许出现遗漏匹配的情况。
- `for ... range` 语句会返回一对「索引/值」。要想只获取索引很容易（忽略值就好）；但若要只获取值，则需要显式声明。在我看来，这种做法更应该颠倒过来，因为在大多数情况下，我更需要值而不是索引。
- 语法：
  - 定义与用途存在不一致。
  - 编译器有时会很挑剔（例如，要求或禁止尾随逗号）；通过良好的工具可以缓解这种困扰，但是有时仍然会产生一些恼人的额外步骤。
  - 使用多值返回类型时，类型上需要括号，但 `return` 语句中却不需要。
  - 声明一个结构体需要两个关键字（`type` 和 `struct`）。
  - 采用大写命名法来标记公共或私有变量，看起来就像匈牙利命名法那样，但更糟糕。
- 隐式接口。我知道它也出现在我喜欢的东西中，但有时候它确实很惹人烦——特别是当你试图找出所有实现该接口的类型，或者哪些接口是为给定类型而实现的时候。
- 你无法在不同的包中编写带有接收器的函数，所以即使接口是「鸭子类型」的，你也不能为其他包中的类型实现这个接口，这使得它们的用处大大降低。

I've already mentioned the lack of generics and macros above.

还有我之前已经提过的，Go 缺少泛型和宏。

## Consistency 一致性

As a language designer and a programmer, probably the thing that most surprised me about Go is the frequent inconsistency between what is built-in and what is available to users. It has been a goal of many languages to eliminate as much magic as possible, and make built-in features available to users. Operator overloading is a simple, but controversial, example. Go has a lot of magic! And you very easily run into the wall of not being able to do things that built-in stuff can.

作为一名语言设计者和程序员，Go 最让我惊讶的地方也许是它的内置功能和用户可用功能之间频频出现不一致。许多语言的目标之一就是尽可能消除编译器魔法，让用户也能使用内置功能。运算符重载是一个简单但有争议的例子。但 Go 有很多魔法！你很容易就会遇到这样的问题: 无法做那些内置功能可以做的事情。

Some things that stood out to me:

一些让我印象深刻的地方：

- There is nice syntax for returning multiple values and for channels, but the two cannot be used together because there are no tuple types.
- There is a `for ... range` statement for iterating over arrays and slices, but you can't iterate over other collections because there is no concept of iterators.
- Functions like `len` and `append`, are global, but there is no way to make your own functions global. Those global functions only work with built-in types. They can also be generic, even though Go has 'no generics'!
- There is no operator overloading, this is particularly annoying with `==` because it means you can't use custom types as keys in a map unless they are _comparable_. That property is derived from the structure of a type and can't be overridden by the programmer.

- 返回多个值和信道的语法很棒，但是这两个无法一起使用，因为没有元组类型。
- 能够用 `for ... range` 语句对数组和切片进行迭代，但对其他集合就无能为力了，因为它缺乏迭代器的概念。
- 像 `len` 或者 `append` 这样的函数是全局函数，但你自己的函数却无法转变成全局函数。这些全局函数只能使用内置类型。即便 Go「没有泛型」，它们也可以变得通用。
- 没有运算符重载，那么 `==` 就会使人感到恼火。因为这意味着你不能在词典中使用自定义类型作为键，除非它们是可比较的。这一属性派生自类型结构，程序员无法重写该属性。

## Conclusion 总结

Go is a simple, small, and enjoyable language. It has some odd corners, but is mostly well-designed. It is incredibly fast to learn, and avoids any features which are not well-known in other languages.

Go 是一种简单、小巧、令人愉悦的语言。它也有一些犄角旮旯，但绝大部分是经过精心设计的。它的学习速度令人难以置信，并且规避了其他语言中一些不那么广为人知的特性。

Go is a very different language to Rust. Although both can vaguely be described as systems languages or 'replacements' for C, they have different goals and applications, styles of language design, and priorities. Garbage collection is a really huge differentiator. Having GC in Go makes the language much simpler and smaller, and easy to reason about. Not having GC in Rust makes it _really_ fast (especially if you need guaranteed latency, not just high throughput), and enables features and programming patterns which are not possible in Go (or at least not without sacrificing performance).

Go 也是一种与 Rust 截然不同的语言。虽然两者都可以笼统地描述为「系统语言」或「C 语言的替代品」，但它们的设计目标、应用领域、语言风格和优先级不尽相同。垃圾收集确实带来了一个巨大的差异：使用 GC 使得 Go 变得更简单、更小，也更容易理解。而不使用 GC 使 Rust 奇快无比（特别是在您需要保证延迟，而不仅仅是高吞吐量的时候），并且得以支持 Go 中不可能实现的特性或编程模式（或者至少在不牺牲性能的前提下是无法实现的）。

Go is a compiled language with a well-implemented runtime. It is fast. Rust is also compiled, but has a much smaller runtime. It is _really fast_. Assuming no other constraints, I think the choice between using Go and Rust is a trade-off between a much shorter learning curve and simpler programs (which means faster development), versus Rust being really, really fast, and having a more expressive type system (which makes your programs safer and means faster debugging and error hunting).

Go 是一种编译型语言，其运行时得到了良好的实现，其速度毋庸置疑。Rust 也是编译型语言，但是运行时要小得多，它真的迅捷无比。在没有其他限制的情况下，我认为选择使用 Go 还是 Rust 其实意味着一种权衡：一方面，Go 的学习曲线更短、程序更简单（这意味着更快的开发速度）；另一方面，Rust 真的性能卓越，并且类型系统更富有表现力（这使程序更安全，也意味着更快的调试和错误查找）。
