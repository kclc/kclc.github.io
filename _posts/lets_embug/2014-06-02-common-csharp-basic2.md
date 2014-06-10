---
layout: post
title: C# の基本的な使い方2
date: 2014-06-10
tags: [ 共通基礎編 ]
---

前回の続きです。

## いろいろな制御文

ここからは、プログラムの流れを制御するのに欠かせない制御文を紹介していきます。

### if 文

if 文は「if」という言葉の指す通り、「もしXXならばYYする」という意味の制御文です。

if 文は次のように書きます。

{% highlight csharp %}
if(bool型の式)
{
    式がtrueの時の処理;
}
{% endhighlight %}

また、false だった時の処理も書くことができます。

{% highlight csharp %}
if(bool型の式)
{
    式がtrueの時の処理;
}
else
{
    falseの時の処理;
}
{% endhighlight %}

さらに、false だった場合にまた条件をつけることもできます。

{% highlight csharp %}
if(bool型の式)
{
    式がtrueの時の処理;
}
else if(bool型の式2)
{
    式2がtrueの時の処理;
}
{% endhighlight %}

これらを組み合わせるとこんなことができます。

{% highlight csharp %}
var input = Console.ReadLine();

if(input == "y" || input == "Y")
{
    Console.WriteLine("Yes!");
}
else if(input == "n" || input == "N")
{
    Console.WriteLine("No!");
}
else
{
    Console.WriteLine("どっちでもないです。");
}
{% endhighlight %}

これの動作を自分で想像して、実際に確かめてみましょう。

### for 文

現在執筆中...
