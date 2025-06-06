# 引言

> “代码更像是‘指导原则’，而不是实际规则。” —— 赫克托·巴博萨

在众多现代编程语言的拥挤景观中，Rust 与众不同。Rust 提供了编译语言的速度，非垃圾回收语言的高效，以及函数式语言的类型安全 —— 同时还提供了解决内存安全问题的独特方案。因此，Rust 经常被评为[最受欢迎的编程语言]。

Rust 的类型系统的强大和一致性意味着，如果一个 Rust 程序能够编译，那么它已经有一个不错的机会可以正常工作 —— 这种现象之前只在更学术、更不亲民的语言中观察到，如 Haskell。如果一个 Rust 程序能够编译，它也将安全地工作。

然而，这种安全 —— 包括类型安全和内存安全 —— 确实是有代价的。尽管基本文档的质量很高，Rust 还是因为入门坡度陡峭而闻名，新来者必须经历与借用检查器的斗争、重新设计数据结构以及被生命周期搞糊涂的入门仪式。一个能够编译的 Rust 程序可能第一次就有很大的机会正常工作，但是为了让它编译的斗争是真实的 —— 即使 Rust 编译器的错误诊断非常有帮助。

## 本书面向的读者

本书试图为在这些领域挣扎的程序员提供帮助，即使他们已经具有像 C++ 这样的现有编译语言的经验。因此，与其他 Effective 系列书籍一样，这本书旨在成为 Rust 新手的第二本所需书籍，在他们已经在其他地方遇到基础知识之后 —— 例如，在 [Rust book]（Steve Klabnik 和 Carol Nichols，No Starch Press）[^1] 或《[Rust 程序设计（第2版）]》（Jim Blandy 等，O'Reilly）[^2] 中。

然而，Rust 的安全性导致这里的条款有一些不同的侧重点，特别是与 Scott Meyers 的原始 Effective C++ 系列相比。C++ 语言充满了陷阱，所以 Effective C++ 专注于避免这些陷阱的一组建议，这些建议基于在 C++ 中创建软件的实际经验。重要的是，它包含的是指导原则而不是规则，因为指导原则有例外 —— 提供指导原则形成及使用的理由，允许读者自行决定特定情况下是否值得违反规则。

在这里，提供建议及其原因的风格被保留了下来。但是，由于 Rust 几乎没有陷阱，这里的条款更多地集中在 Rust 引入的概念上。许多条款的标题像“理解…”和“熟悉自己了解…”，并帮助在编写流畅、地道的 Rust 代码的旅程中。

Rust 的安全性也导致完全没有标题为“永远不要…”的条款。如果你真的不应该做某事，编译器通常会阻止你这样做。

## Rust 版本

文本是为 2018 版的 Rust 编写的，使用稳定工具链。Rust 的后向兼容性承诺意味着任何更高版本的 Rust，包括 2021 版，仍然会支持为 2018 版编写的代码，即使那个更高版本引入了破坏性更改。Rust 现在也足够稳定，以至于 2018 版和 2021 版之间的差异很小；书中没有任何代码需要更改才能符合 2021 版（但是[第 19 条]包括一个例外，其中较晚版本的 Rust 允许以前不可能的新行为）。

这里的条款没有涵盖 Rust 的任何异步功能方面，因为这涉及到更高级的概念和不那么稳定的工具链支持 —— 使用同步 Rust 已经有足够多的内容要介绍了。也许将来会出现一本《有效的异步Rust》…

用于代码片段和错误信息的具体 `rustc` 版本是 `1.70`。代码片段不太可能需要针对更高版本进行更改，但错误消息可能会因你特定的编译器版本而有所不同。包含在文本中的错误消息也已经手动编辑，以适应书的宽度限制，但除此之外都是编译器生成的。

文本中有许多对其他静态类型语言的引用和比较，如 Java、Go 和 C++，以帮助有这些语言经验的读者定位自己。（ C++ 可能是最接近等价的语言，特别是当 C++11 的移动语义发挥作用时。）

## 本书导读

本书的章节构成分为六章：
- 第一章 —— 类型：围绕 Rust 核心类型系统的建议
- 第二章 —— Trait：关于使用 Rust Trait 的建议
- 第三章 —— 概念：构成 Rust 设计核心思想的观念
- 第四章 —— 依赖性：关于使用 Rust 包生态系统的建议
- 第五章 —— 工具：通过超越 Rust 编译器来改进代码库的建议
- 第六章 —— 超越标准 Rust：当你需要在 Rust 标准、安全环境之外工作时，给出的建议

虽然“概念”章节可能比“类型”和“Trait”章节更为基础，但它故意放在书的后面，以便从头到尾阅读的读者可以首先建立一些信心。


## 本书中使用的约定

本书使用了以下排版约定：

- 斜体：表示新术语、URL、电子邮件地址、文件名和文件扩展名。
- 固定宽度：用于程序列表，以及在段落中引用程序元素，如变量或函数名、数据库、数据类型、环境变量、语句和关键字。

以下标记用于标识以某种方式不正确的代码。


| Ferris                                                                  | 含义                         |
| ----------------------------------------------------------------------- | ---------------------------- |
| <img src="./images/ferris/does_not_compile.svg" style="zoom:5%;" />     | 这段代码无法编译！           |
| <img src="./images/ferris/not_desired_behavior.svg" style="zoom:5%;" /> | 这段代码没有产生期望的行为。 |

## 致谢

我要感谢那些帮助使这本书成为可能的人们：
- 技术审阅者们对文本的所有方面提供了专业和详细的反馈：Pietro Albini, Jess Males, Mike Capp，尤其是 Carol Nichols。
- 我在 O'Reilly 的编辑们：Jeff Bleiel, Brian Guerin 和 Katie Tozer。
- Tiziano Santoro，我从他那里最初学到了许多关于 Rust 的知识。
- Danny Elfanbaum，他提供了处理书籍 AsciiDoc 格式化的重要技术支持。

- 原始网络版书籍的勤奋读者们，特别是：
    - Julian Rosse，他在在线文本中发现了数十个拼写错误和其他错误。
    - Martin Disch，他指出了多个条款中可能的改进和不准确之处。
    - Chris Fleetwood, Sergey Kaunov, Clifford Matthews, Remo Senekowitsch, Kirill Zaborsky，以及一位匿名 Proton Mail s用户，他们指出了文本中的错误。
- 我的家人，他们忍受了许多我因写作而分心的周末。

原文[点这里](https://www.lurklurk.org/effective-rust/preface.html)查看

## 注释
[^1]: 国内已由电子工业出版社引进翻译并上市：《[Rust 权威指南（第 2 版）](https://www.phei.com.cn/module/goods/wssd_content.jsp?bookid=66818)》。
[^2]: 国内已由人民邮电出版社引进翻译并上市：《[Rust 程序设计（第 2 版）](https://www.ituring.com.cn/book/2846)》。

<!-- 参考链接 -->

[最受欢迎的编程语言]: https://survey.stackoverflow.co/2022#most-loved-dreaded-and-wanted-language-love-dread
[Rust book]: https://doc.rust-lang.org/book/
[Rust 程序设计（第2版）]: https://www.oreilly.com/library/view/programming-rust-2nd/9781492052586/

[第 19 条]: chapter_3/item19-reflection.md

