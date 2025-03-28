# 概念

本书的前两章涵盖了 Rust 的类型和 trait，这有助于提供编写 Rust 代码所需的一些概念词汇 —— 这正是本章的主题。

借用检查器和生命周期检查是 Rust 独特之处的核心；它们也是 Rust 新手常见的绊脚石，因此是本章前两个条款的重点。

本章的其他条款涵盖了一些更容易理解但与其他语言编写代码略有不同的概念。这包括以下内容：
- 关于 Rust 的 `unsafe` 模式及其避免方法的建议（[第 16 条]）
- 关于在 Rust 中编写多线程代码的好消息和坏消息（[第 17 条]）
- 关于避免运行时终止的建议（[第 18 条]）
- 关于 Rust 反射方法的信息（[第 19 条]）
- 关于平衡优化与可维护性的建议（[第 20 条]）

尝试将你的代码与这些概念的后果对齐是一个好主意。在 Rust 中重现（部分）`C/C++` 的行为是可能的，但如果你这样做，为什么还要麻烦使用 Rust 呢？

## 注释

原文[点这里](https://www.lurklurk.org/effective-rust/concepts.html)查看

<!-- 参考链接 -->

[第 16 条]: chapter_3/item16-unsafe.md
[第 17 条]: chapter_3/item17-deadlock.md
[第 18 条]: chapter_3/item18-panic.md
[第 19 条]: chapter_3/item19-reflection.md
[第 20 条]: chapter_3/item20-optimize.md
