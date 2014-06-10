---
layout: post
title: はじめての C# 
date: 2014-06-03
tags: [ 共通基礎編 ]
---

今回は、C# でのプログラミングの基礎を学習していきます。

### 今回の目標

* C# でプログラムを書く雰囲気をつかむ

* C# のプログラムの構造を理解する。

----

## 雰囲気をつかむ：とりあえず、動かしてみる

まずはプログラムが自分の書いたとおりに動くということを実感してみましょう。

前回作った「KclcFirst」を開いてみてください。

{% highlight csharp linenos %}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace KclcFirst
{
    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
{% endhighlight %}

なにも出ずに終了してしまうのは本当に悲しいので、とりあえずなにかをさせてみましょう。

幸い、はじめてプログラミング言語を触るときに、必ずコレをさせる！というものがあります。

それは「Hello, World!」という名前のプログラムで、その名の通り「Hello, World!」とプログラムに表示させるのです。

「Hello, World!」とプログラムに表示させるには、

{% highlight csharp %}
static void Main(string[] args)
{% endhighlight %}

の下の { と } の中に、次の文字列を追加します。

{% highlight csharp %}
Console.WriteLine("Hello, World!");
{% endhighlight %}

Console とは「コンソール」のことで、実行すると出てくる黒い画面のことです。

WriteLine とは英語でそのまま「一行書き込む」という意味で、文字を表示し、改行しなさい、という命令です。

そして "Hello, World!" が表示したい文字列です。 C# では文字列を "" (２つのダブルクォーテーション)で囲うことで、これは命令ではなくて文字列だとコンパイラに教えてあげます。

つまり、

{% highlight csharp %}
Console.WriteLine("Hello, World!");
{% endhighlight %}

を日本語に直すと、

「コンソール（黒い画面）に「Hello, World!」と表示して、改行しなさい」

という意味になります。わかりやすいでしょ？

これを書き加えたあと、プログラムはこうなっているはずです。

{% highlight csharp linenos %}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace KclcFirst
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello, World!");
        }
    }
}
{% endhighlight %}

さて、実行してみましょう。実行は F5 でしたね(MonoDevelop では違いますが、設定のキーバインドで「Visual Studio」設定を選ぶと同じにできます)。

一瞬「Hello, World!」と表示されて消えてしまいましたね。これでは消えるのが早すぎて読めません。

そこで、なにかが入力されるまで終了しないようにしてみましょう。

「一行書き込む」WriteLine があるなら、「一行読み込む」ReadLine がある気がしますね。

すぐ下に、

{% highlight csharp %}
Console.ReadLine();
{% endhighlight %}

と書き足してみましょう。

Console.ReadLine は、「改行がある（エンターキーを押す）まで文字を読みこむ」という命令です。

文字を表示するわけではないので、カッコの中に文字列は書きません。

今、プログラムはこうなっているはずです。

{% highlight csharp %}
// (略)
        static void Main(string[] args)
        {
            Console.WriteLine("Hello, World!");
            Console.ReadLine();
        }
// (略)
{% endhighlight %} 

実行してみましょう。黒い画面、いやコンソールと呼びましょう。コンソールは消えませんね。改行を押すと消えます。

Console.ReadLine は「改行があるまで文字を読み込む」命令ですが、エンターキーを押されるまで文字を読み込み続けるので、「エンターキーを押されるまで待機」という意味でも使えるというわけです。

さて、Console.WriteLine の中の "" の中の文字を変えてみて、変えたとおりに表示される文が変わるのを確認してみてください。

Console.ReadLine で読み込んだ文字列をどうやって表示するかって？それは後ほど。

----

## C# の構造

### おまじない無しで覚えよう

プログラミングの学習サイトでは、よく「おまじない」という表現が用いられます。

その時解説しにくいものを後回しにするために、これを書いておけば動くという「おまじない」としておくのです。

しかしこれはプログラミングの本質を理解するのにとてもよくありません。

そこで、ここでは「おまじない」を一切使わずに C# の基本を学習していきましょう。

では、「KclcFirst」をもう一度 Visual Studio または MonoDevelop で開きましょう。

{% highlight csharp linenos %}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace KclcFirst
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello, World!");
            Console.ReadLine();
        }
    }
}
{% endhighlight %}

はい。全然意味がわかりませんね。でも大丈夫、次のことを覚えるだけでグッと理解可能になります。

### { と } は構造を表す

謎の記号、{ と }。これはプログラムの構造を表しています。

ここから、次のことがなんとなくわかるでしょう。

* using なんちゃら と namespace なんちゃら は同じ階層にいる

* class なんちゃら は自分だけの階層を持っている

* static void Main(なんちゃら) は自分だけの階層をもっている

* Console.WriteLine("Hello, World!") は一番内側にいて、Console.ReadLine()と仲間である。

同じ階層にいる物体はとても関わりが深いです。外側から攻めて行きましょう。

### using と namespace

namespace はそのまま「名前空間」と言います。これは、プログラムを役割によって分類しておくためのものです。

例えば、「System」名前空間には、基本的な機能がすべて用意されていて、「System.Text」には文字列を処理するための機能、「System.Drawing」は画像などを司るものです。

他の名前空間にある機能は使うことができませんが、「using」と書いてその後に名前空間の名前を書くことで使えるようになります。

例えばさっき無意識に使っていた「Console.WriteLine」は「System」名前空間に所属していますが、「using System;」と書くことで使えるようになっていました。

「using」を使わないと、「System.Console.WriteLine」というように本来の位置を示さないと使うことができません。この書き方を「完全修飾名」と言います。

試しに「Console.WriteLine」を「System.Console.WriteLine」と書き換えてみて、全く同じように動くことを確認してみてください。

### class

class はそのまま「クラス」と言い、namespace よりも更に細かい分類をするのに使います。

例えば、「Console」クラスは、コンソールに関する機能（読み込み、書き込み、リセット）がまとめられています。

また、クラスの特徴として、「インスタンス」というものを作ることができるというものがあります。

「インスタンス」の作り方は後述しますが、この機能を使うと、「同じ機能を持つ」物体を大量に作ることができます。

これについては続編の「オブジェクト指向編」で詳しく解説します。

### メソッド

「メソッド」は、単一の機能をまとめるための単位です。

「static void Main」というのは、「Main という名前のメソッドだよ」というのを表しています。

また、「(string[] args)」というのは、「呼び出すときに string[] という型の式を渡さないといけないよ」という意味です。

（「型」と「式」についてはすぐ後に出てきます。）

例えば、「Console」クラスの「WriteLine」メソッドは、「文字を出力して改行する」という機能を提供します。

メソッドは複数の命令を持つことができ、メソッドを作ることで「他の命令を使って新しい命令を作る」ことができます。

同じメソッドが複数の機能を持つ、というのは良いことではなく、ひとつのメソッドがひとつの機能を持つようにすることが推奨されます。

これについても、「オブジェクト指向編」で詳しく解説します。

### 式

Console.WriteLine("Hello, World!") や Console.ReadLine() の仲間を「式」と言います。

式の仲間には、

* リテラル ... 「"a"」 や 「1」 のように、それ単体で数や文字列を表す。
* 呼び出し ... 「Console.WriteLine」のように、「()」（かっこ）をつけて使い、他の「メソッド」を呼び出して結果を手に入れる。
* 初期化 ... 「new クラスの名前()」という形をしており、呼び出しに似ているが、そのクラスの「インスタンス」を作って返す。
* 演算 ... 「+」や「-」などの「演算子」と呼ばれるものを式に使い、式を変形させる（足し算引き算など）。 
* 変数 ... 「x」や「count」というような様々な名前を持ち、リテラルや呼び出しの内容を保存しておける入れ物のようなもの。

などがあります。

また、式は「型」というものを持っていて、文字列は「文字列型」、整数は「整数型」という具合に、それぞれ違うものとして扱われます。

代表的な型は次のとおりです。

* int 型 ... 整数型。-2,147,483,648~2,147,483,647 の範囲の数を表せる。
* long 型 ...  整数型だが、もっと桁数が多い数を扱える。
* string 型 ... 文字列型。
* char 型 ... 文字型。string 型は char 型の配列である。（配列については後述）
* float 型 ... 実数型。小数点を扱うことができる。 double 型はその名の通り精度が二倍。
* void 型 ... 値を持たない。他のメソッドに渡して使うこともできない。
* bool 型 ... true（真）かfalse（偽）の2つの値のみを持つ。

また、クラスを宣言するとそれを「クラス型」として使うことができます。

実は string 型は System 名前空間の「String」クラス型の別名です。このように、クラスを宣言するとそれを新たな型として扱うことができます。

また、同じ型のものは同じものとして扱うことができます。

例えば、 "Hello, World!" は文字列を表しているので文字列型で、Console.ReadLine() は文字列を読み込むので文字列型です。

つまり、Console.ReadLine() と "Hello, World!" は両方文字列を表すので、ものとしては「同じ」なのです。つまり、

{% highlight csharp %}
Console.WriteLine(Console.ReadLine());
{% endhighlight %}

ということができそうですね？はい、できます。どうなるかは試してみてください（上に書いてある日本語での意味を組み合わせてみれば想像はつきますね？）。

しかし、

{% highlight csharp %}
"Hello, World!";
{% endhighlight %}

ということはできません。これはエラーになります。なぜでしょうか？実は、隠されたもうひとつの種類があるのです。

### 文

「文」は「式」とは違うもので、メソッドを構成する最小単位です。

代表的な文は、

* 宣言文 ... 「int count;」などと書き、「指定された型の変数を使います」と宣言することにより後のコードで使えるようにする。
* 代入文 ... 「count = 1;」などと書き、変数に式の結果を保存する。
* 制御文 ... 「if」や「for」などがあり、繰り返しや分岐など、プログラムの流れを制御するのに使う。

などです。式のなかでは「呼び出し」と「初期化」などのみが文として扱え、それ以外は文として扱うことはできません。

そして、メソッドは複数の文から構成されるので、

{% highlight csharp %}
"Hello, World!";
{% endhighlight %}

のように文ではない「リテラル」をポンと書くことはできないということなのです。

なお、文の終わりには「;」（セミコロン）を書くという決まりがあります。

### まとめ

* 名前空間」の中には「クラス」が入っており、「クラス」の中には「メソッド」が入っており、「メソッド」は複数の「文」で構成され、「文」は「式」を使って様々な命令をすることができる。
* 「using」を使うことで他の「名前空間」のクラスを使うことができる。

なになに？覚えることが多すぎる？大丈夫、古いことわざ曰く、「案ずるより産むが易し」と。

次回からは、今日覚えたことを使って簡単なプログラムを書いてみましょう。
