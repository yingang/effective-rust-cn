# 类型

这本书的第一部分涵盖了关于 Rust 类型系统的建议。Rust 的类型系统比其他主流语言的表达能力更强；它与“学术性”语言如 [OCaml] 或 [Haskell] 有更多共同点。

其中核心的一部分是 Rust 的枚举类型（`enum`），它比其他语言中的枚举类型具有更强的表达能力，并且允许使用[代数数据类型]。

本章的内容涵盖了 Rust 语言的基本类型，以及如何将它们组合成数据结构，来更精确地表达程序的语义。将行为编码到类型系统中的概念有助于减少检查和错误路径代码量。无效的状态会在编译时被编译工具链暴露出来，而不用等到程序运行时。

接下来还介绍了 Rust 标准库中提供的一些随处可见的数据类型：`Option`、`Result` 和 `Iterator`。熟练掌握这些标准工具可以帮助你写出简洁高效、符合 Rust 习惯的代码——尤其是问号操作符的使用，提供了非常简洁优雅且依然类型安全的错误处理。

请注意，涉及 Rust trait 的内容将在下一章中介绍，但因为 trait 描述了类型的行为，因此与本章的内容有一定的重叠。

## 注释

原文[点这里](https://www.lurklurk.org/effective-rust/types.html)查看

<!-- 参考链接 -->

[OCaml]: https://ocaml.org/
[Haskell]: https://www.haskell.org/
[代数数据类型]: https://en.wikipedia.org/wiki/Algebraic_data_type
