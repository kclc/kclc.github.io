---
layout: post
title: C# の基本的な使い方2
date: 2014-06-14
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

## while 文

while 文は「条件が真の間命令を繰り返す」という意味です。

{% highlight csharp %}
while(bool型の式)
{
    式がtrueの間の処理;
}
{% endhighlight %}

例えば、

{% highlight csharp %}
while(true)
{
    Console.Write("あ");
}
{% endhighlight %}

とすると無限に「あああああああ...」と出力することができます。

if 文と組み合わせれば条件を満たすまでリトライすることができます。

下のコードの動作を予想して、実際に試してみましょう。

{% highlight csharp %}
var flag = false;

while(flag == false)
{
    Console.WriteLine("qと入力すると終了します");
    if(Console.ReadLine() == "q")
    {
        flag = true;
    }
}
{% endhighlight %}

また、while のように複数回繰り返す命令文では、```continue``` と ```break``` という特別な命令を用いることができます。

```continue``` は、処理を全部スキップして次の周回に進みます。

```break``` は、その場で即繰り返しを終了します。

これを使うと、先のコードはこのように書きなおすことができます。

{% highlight csharp %}
while(true)
{
    Console.WriteLine("qと入力すると終了します");
    if(Console.ReadLine() == "q")
    {
        break;
    }
}
{% endhighlight %}

また、 do-while 文というものがあり、たとえ条件が最初から偽でも、必ず一回は実行させることができます。

{% highlight csharp %}
do
{
    Console.WriteLine("一回は必ず表示");
}
while(false);
{% endhighlight %}

これを使うと、最終的にはここまでシンプルに書けます。

{% highlight csharp %}
do
{
    Console.WriteLine("qと入力すると終了します");
}
while(Console.ReadLine() != "q");
{% endhighlight %}

## for 文

for 文は少し複雑です。

for 文は

{% highlight csharp %}
for(カウンタ変数の宣言式; 条件式; カウンタ変数の更新式)
{
    実行する処理;
}
{% endhighlight %}

このように書き、

{% highlight csharp %}
カウンタ変数の宣言式;

while(条件式)
{
    実行する処理;
    カウンタ変数の更新式;
}
{% endhighlight %}

と同じ意味となります。

for文だけはえらくややこしく、定義を見ただけでは全然理解できないので、実際に使ってみましょう。

{% highlight csharp %}
for(var i = 0; i < 10; i++)
{
    Console.WriteLine(i);
}
{% endhighlight %}

これを実行してみましょう。コンソールに0〜9までの文字列が表示されましたね？

{% highlight csharp %}
var i = 0;

while(i < 10)
{
    Console.WriteLine(i);
    i++;
}
{% endhighlight %}

と書き換えてみましょう。全く同じように動くことがわかるでしょう。

for 文というものは、ある変数の値（これをカウンタ変数と言います）をどんどん変化させていき、条件を満たす間だけ繰り返すという命令なのです。

for 文を使えば、配列の中身を簡単に全部表示させることができます。

配列の中身は、配列変数の持つメンバーである ```Length``` プロパティを使って取得することができます。

メンバーを使うときは「.」（ドット）を使うんでしたね？

{% highlight csharp %}
var array = new int[]{ 1, 2, 3, 4, 5 };

for(var i = 0; i < array.Length; i++)
{
    Console.WriteLine(array[i]);
}
{% endhighlight %}

これで 1〜5 の数字が表示されるはずです。しかし、もっといいやり方があるのです。

## foreach 文

foreach 文は、配列の中身を一つずつ取り出して、それぞれに対する処理を実行することができる命令文です。

foreach 文はとても簡単で、次のように書きます。

{% highlight csharp %}
foreach(var 要素名 in 配列)
{
    要素を使った処理;
}
{% endhighlight %}

これを使って先ほどのコードを書きなおしてみましょう。

{% highlight csharp %}
var array = new int[]{ 1, 2, 3, 4, 5 };

for(var item in array)
{
    Console.WriteLine(item);
}
{% endhighlight %}

このように、配列の長さなどを全く考えなくていいのでとても楽です。

そのかわり、for 文と異なり、そのままでは現在が何回目の繰り返しなのかを知る手段がないので注意してください。

## switch 文

switch 文は、if 文のさらに便利なバージョンです。

{% highlight csharp %}
switch(式)
{
    case リテラル1:
        リテラル1に等しい時の処理;
    break;

    case リテラル2:
        リテラル2に等しい時の処理;
    break;

    // いくらでも続けることができる

    default:
        どれにも等しくない時の処理;
    break;
}
{% endhighlight %}

このように、式とリテラルが等しいかどうかで簡単に処理を分けることができますが、

「等しいかどうか」を「リテラルとしか」比較できないのが欠点です。

また、複数のリテラルのうちどれかに等しいかどうかを判断したい場合は、```case リテラル:``` を並べて書くことで、

それらのうちどれかに等しかった場合に処理を行うことができます。

これを使うと、一番上の if 文のサンプルはこのように書きかえられます。

{% highlight csharp %}
var input = Console.ReadLine();

switch(input)
{
    case "y":
    case "Y":
        Console.WriteLine("Yes!");
    break;

    case "n":
    case "N":
        Console.WriteLine("No!");
    break;

    default:
        Console.WriteLine("どっちでもないです。");
    break;
}
{% endhighlight %}

## まとめ

このように、同じことをするのにも複数の方法があるのがわかるでしょう。

どの方法を使うと良いかは人によって感じ方が異なるため、実際に使ってみないとわかりません。

これで基本的な C# の解説は終わりです。次回からは今回までで学んだことを使って、いよいよゲームっぽいものを作っていきましょう。
