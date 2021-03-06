---
layout: post
title: C# 開発環境のセットアップ
date: 2014-06-02
tags: [ 共通基礎編 ]
---

では早速、C# の開発環境のセットアップをしていきましょう。

### 今回の目標

* C# を使ってプログラミングできる環境をセットアップする。

* C# の基本的なプログラムが走るかどうか確認する。

----

## Windows の場合

ある程度のスペックがあるパソコンなら、Visual Studio 2013 Express が良いでしょう。

コン部の EeePC はあまりスペックがないので Visual C# 2008 というものが入っていますが、操作はほとんど変わらないので、適宜読み替えてください。

### Visual Studio とは？

Visual Studio は、Microsoft 公式の C# の開発環境です。

Professional 版や Ultimate 版は有料ですが、Express 版は無料で使うことができます。

### インストール方法

[Microsoft の Visual Studio 2013 Express のダウンロードページ](http://www.microsoft.com/ja-jp/download/details.aspx?id=40787)からインストーラをダウンロードしましょう。

回線に余裕がある場合は VS2013_RTM_DskExp_JPN.iso (ISOイメージ、必要なファイルがすべてはいっています)、

回線が遅い場合は wdexpress_full.exe (ウェブインストーラ、インストールの途中に必要なファイルをひとつひとつダウンロードします)をダウンロードするとよいでしょう。

スペックが低い場合は Visual C# 2008 Express を代わりにダウンロードします。

[ウェブインストーラ](http://go.microsoft.com/?LinkId=9348303)と[ISOイメージ](http://go.microsoft.com/?LinkId=9348306)が同様にダウンロードできます。

### 起動してみよう

* 初回起動時に「環境設定」という感じのウィンドウが出てくるので、「C# 推奨設定」を選びましょう。

* 正常に起動すれば、下のような画面が出てくるはずです。

![Visual Studio 2013]({{ site.url }}/assets/img/vs2013.png)

----

## GNU/Linux の場合

### インストールする

GNU/Linux にインストールする場合、ディストリビューションによって異なりますが、たいていは monodevelop パッケージをインストールすることでセットアップできます。

Ubuntu/Debian:

    apt-get install monodevelop

Fedora: 

    yum install monodevelop

Arch:

    pacman -S monodevelop

もし使っているディストリビューションに monodevelop パッケージが無かったり、自分でビルドしたかったりするときは、

    git clone https://github.com/mono/monodevelop.git

とかして、

    ./configure

のエラー出力を見つつ足りないパッケージを揃えましょう。

### MonoDevelop を起動する

Mono は、C# が動作する仮想マシンである .NET ランタイムのオープンソース実装で、

MonoDevelop は Visual Studio の Mono 版と考えて差し支えありません。

実際、どちらで作ったプロジェクトファイルでも両方で開くことができます。

MonoDevelop を起動すると、下のような画面が出るはずです。

![MonoDevelop]({{ site.url }}/assets/img/md.png)

----

## はじめての C# プログラム

では、C# でプログラムを書き始める方法を確認していきましょう。


### ソリューションの作成

Visual Studio でも MonoDevelop でも、「ファイル」->「新規」->「ソリューション」とメニューを選択していきましょう。

「ソリューション」というのは、C# プログラムを書くときの一つの単位です。

しかし、「ソリューション」がプログラムに一対一に対応するわけではなく、「ソリューション」の下に配置される「プロジェクト」がひとつのプログラムになります。

つまり、一つの「ソリューション」は複数の「プロジェクト」、つまり複数のプログラムを含むことができます。ややこしいですが、覚えてください。

メニューを選択して出てきた画面では、ソリューションの一つ目のプロジェクトの形式を聞かれます。

↓Visual Studio 2013 での例

![Visual Studio 2013 での例]({{ site.url }}/assets/img/vs2013_solution.png)

（左側が Visual Studio、右側が MonoDevelop での表記）

* コンソールアプリケーション / コンソールプロジェクト

...ウィンドウを持たずに黒い画面（コンソール）で動作する基本的なプログラム

* クラスライブラリ / ライブラリ

...それ単体では動かない、プログラマに機能を提供するためのプログラム

* Windowsフォームアプリケーション・WPFアプリケーション / Gtk# 2.0 プロジェクト

... ウィンドウを持つプログラム。

ここでは、動作確認のための簡単なプログラムを書きたいので、「コンソールアプリケーション」を選びます。

デフォルトでは名前が「ConsoleApplication1」などになっていると思います。

しかし、ここでは初めてのプログラムという意味を込めて「KclcFirst」にしましょう。

![Visual Studio 2013 での例2]({{ site.url }}/assets/img/vs2013_kclcfirst.png)

おめでとう！これでソリューションを作ることが出来ました。

### プログラムを動かしてみよう

何もしていない状態では、Visual Studio または MonoDevelop は下のような画面になっているはずです。

![Visual Studio 2013 での例3]({{ site.url }}/assets/img/vs2013_editor.png)

中央部分に出ているのがプログラムのコードです。

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

なにがなんだかさっぱりわからないでしょうが、これは「何もしないプログラム」です。

この役立たずプログラムを試しに実行してみましょう。プログラムを実行するには、「F5」ボタンを押します。

押しましたか？しばらく待ったあと、黒い画面が一瞬出てきてすぐ消えませんでしたか？

そうです、彼は「何もしない」という彼に与えられた使命をこなすと、一瞬で消えていきました。

大成功です。ごあんしんください。

もう一回押してみましょう。今度は一瞬で出てきて一瞬で消えていきましたね。

コードはそれ自体では実行できずに、コンピュータが理解できるように翻訳してあげる必要があります。

それをするのが「コンパイラ」と呼ばれるアプリケーションで、翻訳行為は「コンパイル」と呼ばれます。

先程は「コンパイラ」がコードから機械が理解できるプログラムに翻訳したわけですが、今度はすでに翻訳済なので再翻訳する必要がありません。

よって、彼は翻訳をサボりました。さっきよりも起動が速くなったのは、こういうわけです。

彼に仕事を強制させるには、「ビルド」メニューから「リビルド」ボタンを押します。「ビルド」メニューの「ビルド」からは、実行をせずにコンパイルだけを行うことができます。

次回からは、この何もしない役立たずプログラムになんとか仕事をさせてみましょう。
