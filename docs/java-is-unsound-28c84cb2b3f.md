# Java 不健全:行业观点

> 原文：<https://medium.com/hackernoon/java-is-unsound-28c84cb2b3f>

最近[纳达阿明](https://medium.com/u/a01b7ea46ac4?source=post_page-----28c84cb2b3f--------------------------------)和我发现 [Java](https://hackernoon.com/tagged/java) 和 Scala 不健全。我们把这个发现和相关的讨论提交给了 OOPSLA，一个关于面向对象编程的学术会议。很高兴看到纸张在工业界流传，但似乎也有很多混乱，我认为这是我们的错。这篇论文是为学术界写的，所以它没有从工业界的角度讨论这个问题。我现在正在赶一个截止日期，所以让我在这里写一篇针对行业的论文的节略版，只关注 Java。

# “不健全”是什么意思？

大多数类型系统的目标是为一个良好类型的程序的行为提供某种保证。例如，在许多语言中，在类型良好的程序中，所有的内存访问都是“安全的”。如果一个类型系统实际上成功地提供了这种保证，那么它就是健全的。因此，非正式地说，如果一个类型系统确保了它的设计者想要它确保的东西，那么它就是健全的。这很像编程:如果一个程序做了它应该做的事情，它就是正确的。

Java 的类型系统旨在确保如果一个方法需要一个整数，那么它只能得到整数，而不能得到字符串。因此，下面的伪代码被类型系统拒绝:

```
public Integer increment(Integer i) { return i + 1; }
String countdown = increment(“98765432”);
```

当然，在 JavaScript 中这可能是有意义的，但是 Java 的实现方式非常不同，允许这些代码真的会弄乱堆(或者甚至是栈，如果你喜欢一些 C/C++内存管理不当的错误的话)。

现在你可能已经知道 Java 的类型系统有一些不完善的地方。例如，由于历史原因，Java 具有协变数组，因此进行代码类型检查:

```
String[] strs = { "NaN" };
Object[] objs = strs;
objs[0] = 1;
String one = strs[0];
```

当添加泛型时，Java 使用“原始类型”,这样泛型化的代码可以与前泛型代码兼容。因此，以下类型的检查:

```
List<Integer> ints = Arrays.asList(1);
List raw = ints;
List<String> strs = raw;
String one = strs.get(0);
```

因此，这两个例子似乎都允许`one`包含一个`Integer`，尽管事实上它被声明为具有类型`String`。

现在这让我们回到意图。设计者*希望*类型系统允许这种行为。这是因为，尽管这些例子显然是不好的，但有许多例子表明这种放任是有用的。毕竟，无类型语言就是允许不好的事情发生，这样更酷的事情也可以发生。因为这种行为是有意的，所以设计者是有计划的。每次你赋值给一个数组(引用类型的)，运行时查找数组值的实际元素类型，如果不兼容就抛出一个`ArrayStoreException`。所以在上面的例子中，赋值`objs[0] = 1;`在看似不合理的赋值`String one = strs[0];`到达之前就失败了。类似地，每当在`List<String>`上调用`get`时，运行时检查返回值是否实际上是`String`，以防原始类型被误用，否则抛出`ClassCastException`。

因此，Java 的类型系统看起来就像预期的那样完善，尽管可能没有您希望的那么完善。自从引入泛型以来，只要你不使用这些有意的后门，它就被认为是“真正”可靠的。

# “真正的”不健康

这是我们最近流传的“真正的”不健全的例子。它将一个`Integer`实例分配给一个`String`变量。根据 Java 规范，这个程序是良好类型的，并且根据 Java 规范，它应该毫无例外地执行*(与前面提到的后门不同)并且*实际上*将`Integer`实例分配给`String`变量，违反了良好类型程序的预期行为。由此说明 Java 的类型系统是不健全的。*

*现在，你，像许多其他人一样，可能被这个例子弄糊涂了，并且可能已经做了一些让你自己更加糊涂的事情。因此，让我首先指出每个常见的混淆点:*

1.  *人们不理解为什么要进行这种类型的检查，甚至主动认为应该进行*而不是*类型的检查。*
2.  *如果您将它复制到您自己的 Java 编译器中，编译器可能会说程序不进行类型检查，这与我的说法相矛盾。*
3.  *如果你的编译器做了类型检查，然后你运行它，你会得到一个`ClassCastException`，这也与我的声明相矛盾。*

*您还想知道为什么这很重要，尤其是因为您和您的同事不太可能编写这样的代码。我将解决所有这些问题，虽然顺序不对。*

# *“但是它不编译”*

*如果你的编译器没有对我们的例子进行类型检查，我有消息告诉你。不，你的编译器没有捕捉到错误。其实你的编译器本身就有 bug。你的编译器坏了。Java 规范说这个例子应该进行类型检查和编译。您的编译器应该实现该规范，但它在这里失败了。它失败了，因为它没有预料到我们在这里创造的极限情况。*

# *“但这只是一个角落的情况”*

*你处理过的 bug 有多少是死角案例？一个好的程序员应该预见并处理极限情况，而不是仅仅因为一个 bug 很难创建就原谅它。当然，有时资源是有限的，您可能决定 bug 是低优先级的，但是您只能在识别它之后评估它的优先级。因此，即使这个 bug 被证明是低优先级的(我稍后会谈到)，知道它的存在仍然很重要。*

# *“但会引发异常”*

*感谢上帝，这纯粹是因为运气好！还记得对`List<String>`上的`get`的调用如何秘密地检查返回值实际上是一个`String`吗？这种秘密检查是为了向后兼容原始类型。当程序中没有原始类型时，这应该是不必要的。但是多亏了它，当我们的例子运行时总是抛出一个`ClassCastException`(如果你的编译器足够聪明来编译它的话)。*

*因此，如果历史稍有不同，无论是 Sun 在添加泛型后决定放弃向后兼容性，还是 Sun 将泛型添加到 JVM 中，或者 Java 首先与泛型一起发布，都不会抛出这个异常。相反，我可以将任何东西转换成一个`int[]`，并直接访问许多对象的原始字节，然后我可以用它来注入任意代码(使用[面向返回的编程](https://en.wikipedia.org/wiki/Return-oriented_programming)来绕过安全措施)。*

# *“但是没有人会写这个”*

*你可能永远不会写这个，你的同事也不会写这个。这种推理适用于许多情况。我实际上做这个[所有的](http://www.cs.cornell.edu/~ross/publications/mixedsite/)T10 时间[时间](http://www.cs.cornell.edu/~ross/publications/chpeffects/)；这是我研究议程的一大部分。但是你必须小心应用它的地方。健全是一种安全保证，而不是可用性问题。重要的是是否有人能写这个，因为这样某人就能绕过人们信任的安全措施，做他们想做的任何事情。在健全的情况下，你应该担心的是恶意的程序员，而不仅仅是你和你的朋友。*

# *“但是代码不应该进行类型检查”*

*许多人认为类型`Constrain<U,? super T>`应该是无效的，因为`Constrain`要求其第二个类型参数是其第一个类型参数的子类型，但是`T`和`T`的每个超类型都不是`U`的子类型。但是这种推理混淆了无效性和不变性。事实上，这种错误的推理至少在我高中毕业的时候就已经存在于工业界和学术界了(这已经有一段时间了)。*

*这是一个更简单的谬论:*

```
*class Foo<T extends Number> {
    Number foo(T t) { return t; }
}*
```

*`Foo<String>`是有效类型安全吗？例如，下面的代码安全吗:*

```
*Number bar(Foo<String> foos) { return foos.foo("NaN"); }*
```

*到目前为止，传统的观点，可能还有你的直觉，会说这是不安全的，因为它把一个`String`变成了一个`Number`，但事实是它是完全安全的。这里有一个等价的程序来说明为什么:*

```
*interface IFoo<T> {
    Number foo(T t);
}class Foo<T extends Number> implements IFoo<T> {
    public Number foo(T t) { return t; }
}Number bar(IFoo<String> foos) { return foos.foo("NaN"); }*
```

*对于任何带有约束类型参数的类，我可以创建一个没有约束的相应接口，并在整个程序中使用它。这将与原始程序的行为相同。(对此有一些澄清，但我会把它们留给[论文](https://raw.githubusercontent.com/namin/unsound/master/doc/unsound-oopsla16.pdf)。)*

*那么为什么看起来`Foo<String>`应该是无效的呢？怎么是`bar`安全？嗯，这两个问题的答案是一样的:`Foo<String>`是不可描述的。您将永远无法创建`Foo<String>`的实例，因为`String`不是`Number`的子类型。因此在`bar`中看似不安全的`foo`调用永远不会发生，因为你不能调用一个永远不存在的对象的方法。*

*因此，根据同样的推理，对于`Constrain<U,? super T>`来说是完全安全有效的。只有在运行时`T`是`U`的子类型，满足约束条件时，才能拥有它的实例。*

*但是`Constrain<U,? super T>`在 Java 中是不存在的，因为`null`存在于每一个引用类型中。所以当我解释为什么这个程序类型检查时，请记住这一点。*

# *通配符捕获*

*Java 通配符`?`不是类型。它只是一段表示未知事物的语法。不同的通配符可以代表不同的未知类型。所以为了推理通配符，Java 使用了一个叫做*通配符捕获*的过程。*

*假设我们有一个类型为`Constrain<U,? super T>`的表达式 *e* 。此表达式的类型中有一个通配符。类型检查器不知道它代表什么，但是它确实代表了一些东西，所以类型检查器给这个未知的东西一个临时的名字，比如说`X`。此外，类型检查器知道未知的东西至少必须是`T`的超类型。因此，类型检查器将 *e* 视为具有类型`Constrain<U,X>`，其中`X`是`T`的超类型。*

*但是类型检查器知道更多的东西。它知道`X`必须是有效的类型参数。因此，类型检查器也注意到`X`必须是`U`的子类型。我们称之为通配符上的*隐式*约束，而`super T`是通配符上的显式约束。我发现，尽管不常见，但这种隐式约束实际上被用于许多 Java 库的类型检查。论文[给出了一个具体的例子来说明为什么隐式约束是重要的。](https://raw.githubusercontent.com/namin/unsound/master/doc/unsound-oopsla16.pdf)*

*现在再看看这个例子。在对`bind.upcast(constrain, t)`的调用中，类型检查器执行前面提到的通配符捕获过程，并将`constrain`视为具有`Constrain<U,X>`，其中`X`是`T`的超类型(显式)和`U`的子类型(隐式)。因此，它推断出`X`是`bind.upcast`的类型参数，并使用它的显式和隐式约束对调用的其余部分进行类型检查。*

# *谢谢，Null！*

*好吧，如果不可靠型不是不健康的根源，那是什么？令人惊讶的是，空指针不仅会导致程序出错，还会导致类型系统出错！通配符捕获的理由完全忘记了空指针。它假设对于某些`X`必须有一些实际的`Constrain<U,X>`，这一假设在对`X`的隐式约束中表现出来。所以所有这些都归结为一个空指针错误。但是与大多数空指针错误不同，这个错误花了 12 年才被发现。哦，它也不像大多数空指针错误那样容易修复，因为涉及到的每个特性都在实践中使用。但是 Java 团队正在解决这个问题。在你再次坚持认为解决方案是不允许使用`Constrain<U,? super T>`类型之前，要意识到这种推理将核心 Scala 的可靠性证明(没有 null)推迟了整整十年，我并不特别渴望花十年时间来解决这个问题。*

# *附言*

*未来的语言设计师们，请记住这一点！尤其是如果你没有编译成 JVM。Java 很幸运，它受到了向后兼容性的阻碍；你可能没这么幸运。*

> *[黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是 [@AMI](http://bit.ly/atAMIatAMI) 家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)，并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。*
> 
> *要了解更多信息，请[阅读我们的“关于”页面](https://goo.gl/4ofytp)、[在脸书上点赞/给我们发消息](http://bit.ly/HackernoonFB)，或者简单地说， [tweet/DM @HackerNoon。](https://goo.gl/k7XYbx)*
> 
> *如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！*