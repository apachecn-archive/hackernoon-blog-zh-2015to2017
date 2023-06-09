# 为小网站创造更准确的搜索结果！

> 原文：<https://medium.com/hackernoon/creating-more-accurate-search-results-for-small-sites-436e64da79b6>

![](img/3dd2190c342b6328569cb4417c87bbc3.png)

在之前的一篇帖子中，我在一个小网站上工作，在那里你可以搜索唐纳德·特朗普最近的演讲，并获得他使用某些单词或短语的频率、使用它们的时间以及他最经常在哪里说某些事情的统计数据。作为参考，他是我正在建设的网站的工作原型:

[https://trumpspeechdata.herokuapp.com/](https://trumpspeechdata.herokuapp.com/)

现在，假设我想添加一个特性，这样您就可以搜索一个主题，并返回关于该主题的任何演讲。现在，你是否曾经在一个给定的网站上搜索过某样东西，而搜索结果与你实际想要的并不太接近？我们以前可能都遇到过这种情况。如果我们有大量的数据，我要建议的可能不可行，但是对于像这个网站这样的小块数据，它是合理的，并且允许我们返回更准确的搜索结果。

如果你想了解的话，这是我目前掌握的数据:

[https://www . Dropbox . com/s/u 4 vuwazx 609 uvvw/trump speeches . JSON？dl=0](https://www.dropbox.com/s/u4vuwazx609uvvw/trumpspeeches.json?dl=0)

我们当前的数据结构如下所示:

```
{
   "speechtitle": "Title of Speech",
   "speechdate": "Date of Speech",
   "speechlocation": "Location of Speech",
   "text": "Entire transcript of Speech",
}
```

如果用户搜索一个特定的主题，如果他们的搜索与演讲的主题相匹配，我们可能会将所有的数据返回给用户。首先，让我们使用这个用户案例:

用户 Bob 搜索“预算”,这样他可以查看唐纳德·特朗普关于预算的演讲。

我们可以这样做的一个方法是:

```
let matchingSpeeches = [];
for (var i = 0; i < api.length; i++) {
if(api[i].speechtitle.indexOf(inputValue) > -1) {
matchingspeeches.push([
api[i].speechtitle,
api[i].speechdate,
api[i].speechlocation,
api[i].text,
])
  }
}
```

这基本上是说，“如果演讲标题包含要搜索的单词或短语，就将其推入匹配的演讲数组中”。然后，我们将能够向用户格式化数组的结果。说回鲍勃，这会让他得到他想要的吗？可以，只要演讲题目中包含“预算”即可。但是如果有一个关于预算的演讲，但是预算没有出现在演讲标题中呢？对不起，鲍勃，你被解雇了。

也许我们可以做同样的事情，如上所述，但也包括搜索演讲文本，就像这样:

```
let matchingSpeeches = [];
for (var i = 0; i < api.length; i++) {
if(api[i].speechtitle.indexOf(inputValue) > -1 || api[i].text.indexOf(inputValue) > -1) {
matchingspeeches.push([
api[i].speechtitle,
api[i].speechdate,
api[i].speechlocation,
api[i].text,
])
  }
}
```

这里我们说，“好的，如果搜索值出现在演讲的标题或文本中，我们会把它放入数组中。”更好对吗？嗯，是也不是。如果一个演讲都是关于堕胎，或枪支管制，但只提到一次预算呢？这个演讲实际上根本不是关于预算的，但我们还是把它还给鲍勃，让他把这些乱七八糟的东西整理好。或者，如果演讲是关于预算的，但使用了另一个词，如演讲中的“支出”，但实际上并没有提到“预算？”我们可以把我们的用户 Bob 放在一个场景中，他得到一个关于堕胎的演讲，但是没有得到一个关于消费的演讲。这对我们的最终用户来说不是一件好事，鲍勃。这是另一个想法。让我们在数据结构中添加一个名为“tags”的字段。然后，对于每个演讲，我们可以为主题添加标签。例如，让我们从 JSON 数据中取出这个条目:

```
{
   "speechtitle": "Remarks by President Trump at Tax Reform Event",
   "speechdate": "September 2017",
   "speechlocation": "Indiana",
   "text": "speech text here",
}
```

我们可以修改如下:

```
{
   "speechtitle": "Remarks by President Trump at Tax Reform Event",
   "speechtags": ["budget", "taxes"], "speechdate": "September 2017",
   "speechlocation": "Indiana",
   "text": "speech text here",
}
```

然后当 Bob 进行搜索时，我们可以使用前面的代码，循环遍历标签，返回一个匹配搜索输入的标签。然而，即使这可以更有针对性，并且在理论上使我们的搜索结果更好，我们仍然会遇到问题。例如，如果 Bob 搜索“支出”而不是“预算”会怎样。同样，即使他们很接近，这个演讲也不会发送给 bob，因为查询不匹配。这里有一种方法可以解决这个问题。我们想做的是总结出许多流行的搜索术语。因此，如果用户搜索“支出”、“预算”、“税改”或“赤字”，我们仍然会向用户发送带有“预算”标签的结果，因为这是一个非常接近的匹配。我们要做的是构建一个 word 对象。然后，我们可以在对象中放入任何我们想要的单词。该结构看起来会像这样:

```
var mapObj = {
        "a" : "b",
        "c" : "b",
        "d" : "b",
        "e" : "b",
}
```

这里的想法是，如果用户 Bob 搜索“a”，我们会给他“b”。如果他搜索“c”或“d”或“e”，我们还是会给他“b”。这正是我们上面所描述的。基本上，如果他搜索“支出”，我们将返回“预算”。但是如果他搜索“税收改革”或“赤字”或“预算”，我们仍然会返回包含“预算”的结果，因为这仍然是一个很好的匹配。

现在，我们需要添加一些正则表达式来匹配输入字符串。代码可能是这样的:

```
var mapObj = {
        "spending" : "budget",
        "tax reform" : "budget",
        "deficit" : "budget",
        "budget" : "budget",
      };
      var re = new RegExp(Object.keys(mapObj).join("|"), "gi");
      keyWord = str.replace(re, function(matched) {
        return mapObj[matched.toLowerCase()];
      });
```

我们使用 Regex 来匹配用户搜索的内容，然后用其他内容替换它。所以现在我们可以在前面的代码中使用变量“keyWord ”,并使用我们创建的 speechtags 字段:

```
let matchingSpeeches = [];
for (var i = 0; i < api.length; i++) {
if(api[i].speechtags.indexOf(keyWord) > -1) {
matchingspeeches.push([
api[i].speechtitle,
api[i].speechdate,
api[i].speechlocation,
api[i].text,
])
  }
}
```

正如我之前提到的，这在大范围内可能不太管用，但我认为在这种情况下行得通，因为我们的范围非常有限。因为主题是政治，所以用户可能输入的搜索词是有限的。如果我们没有得到任何与用户输入相匹配的内容，我们总是可以放一些代码给用户。例如，如果 Bob 搜索“鸡汤”，我们可能不会有很多数据可用。由于可能的搜索词有些有限，我们可以修改我们的搜索对象，以包括尽可能多的可能性，以匹配我们正在使用的所有标签，如下所示:

```
var mapObj = {
        "spending" : "budget",
        "tax reform" : "budget",
        "deficit" : "budget",
        "budget" : "budget", "abortion" : "abortion",
        "women's rights" : "abortion",
        "pro life" : "abortion",
        "pro choice" : "abortion", "healthcare" : "healthcare",
        "obamacare" : "healthcare",
        "health reform" : "healthcare",
        "medicaid" : "healthcare",
      };
      var re = new RegExp(Object.keys(mapObj).join("|"), "gi");
      keyWord = str.replace(re, function(matched) {
        return mapObj[matched.toLowerCase()];
      });
```

然后我们可以回过头来给每篇演讲添加标签，以匹配我们正在使用的关键词。我们可以手动这样做，尤其是当我们的数据集很小的时候，或者我们可以使用 JavaScript 或 Python 或其他什么，但我不会在这里讨论这些。同样，即使在这种情况下，我们仍然会遇到一些问题，但如果您正在寻找一种快速的方法来使您返回的搜索结果更有针对性，尤其是对于较小的数据集，这并不坏。

[](https://www.upwork.com/freelancers/~01d8efb8f4de6e3911) [## 伊桑·贾雷尔

### 我的背景是平面设计，在过去的 10 年里，我一直在为一家公司做数码和印刷设计

www.upwork.com](https://www.upwork.com/freelancers/~01d8efb8f4de6e3911)