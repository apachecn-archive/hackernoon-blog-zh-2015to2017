# 使用 ScalaCheck 探索基于属性的测试(简单示例)

> 原文：<https://medium.com/hackernoon/exploring-property-based-testing-with-scalacheck-simple-examples-bcdc34600810>

![](img/d03c01214cacb83270e014f23a625e12.png)

> 这是更多的例子而不是谈话。

将 ScalaCheck 添加到您的 *build.sbt* 文件中

第一个问题，FizzBuzz

让我们看一些测试 FizzBuzz 问题。

每个测试都试图证明 FizzBuzz 的某些属性，例如，属性“only div by 3”试图证明 Fizz 仅在传递的值被 3 整除而不是被 5 整除时返回。看看值生成器( *divBy3* )会让我们意识到我们正在过滤掉那些能被 5 整除的值。

按照同样的思路，我们可以证明其他属性，例如只有那些能被 5 整除而不能被 3 整除的属性才应该被翻译成“Buzz”，或者如果值不能被 3 整除和 5 整除，则应该使用 id 函数和 toString 来翻译，这样它们就变成了字符串格式。

这里的神奇之处在于，基于我们的生成器属性，每个测试将使用随机值空间(不稳定)运行至少 100 次。在我看来，这比使用问题域的有限值，比如 5，10，15，2，24，2，来测试更强。

另一方面，这种测试技术不应该取代 TDD，而应该将其扩展为更完整的测试套件。

我们对 FizzBuzz 的实现如下所示。

# 第二个问题，堆栈

现在，让我们看看如何使用相同的技术来测试一个定制的、功能性的堆栈实现。

## 大小

让我们从测试开始，因为它们是我们在这篇文章中关注的领域。

首先，我们定义一个值生成器，专门用于正 int 值。

然后我们定义我们的第一个测试，即*将多个值(按顺序)压入堆栈，并验证堆栈的大小与压入的值的数量相对应。*

记住，相同的测试将运行 100 次，并推送不同数量的值。第一次运行时，可能会推送 2 个值并验证大小为 2，然后可能会再次运行，推送 97 个值并再次验证堆栈的大小为 97。

## 挑选

我们的第二个测试验证了从堆栈中选择不会修改它。

使用相同的原理，测试运行很多次，每次将不同数量的项目推入堆栈，然后调用`.head` ( *pick* )，然后验证大小是否等于被推入的值的数量，这意味着`.head`不修改堆栈。

## toList

现在，我们可以测试获得堆栈的列表表示(不修改堆栈)。

再一次，使用相同的原理，每次测试运行时，它检查`.toList`是否返回我们以相反顺序推送的相同值。

## 推拉式

我们的“推拉”测试验证了我们放入堆栈的任何东西都可以以正确的顺序取出。同样，这个测试将使用不同的堆栈大小运行 100 次。

## 堆

我们的栈是一个不可变的数据结构。对堆栈的操作不会修改它，而是创建新的堆栈。

# 结论

基于属性的测试是一个强大的工具。我发现它在编写复杂的数据结构时非常有用，比如我们已经添加到[](https://github.com/stew/dogs)*中的数据结构。然而，它不应该取代其他技术，如 TDD(测试驱动开发),而是对它们的补充。*