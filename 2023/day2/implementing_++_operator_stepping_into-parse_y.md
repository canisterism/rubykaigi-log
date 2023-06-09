# Implementing ++ operator stepping into parse.y

- `++` はパースの時点で失敗する
- `+` は unaryなので、`++` 数字とかを期待してる
  - のにそこでinputが終わる（Unexpected end of input）
- 流れ
  - Scanner
    - トークンに変える
  - Parser
    - 構文規則の適用  
      - BNFみたいなやつ
- 実現の方法の検討
  - 1. +を.succに変えてみる
    - parse.yに++をsuccに置き換えるルールを追加する
      - succは返り値にインクリメントした値を返すので、レシーバは変わってない
  - 2. `++` メソッド（レシーバを破壊的に変更する）を定義してしまう
    - レシーバの変数のIDが必要なんだけど、レシーバがintegerリテラル（1とか）のときにセグフォしちゃう
  - 3. `+=1`のシンタックスシュガーでよくね？
    - i++ * 2がi += 1 * 2になってしまうので変
      - 優先度を変えるとかで対応できるかもだけどハードすぎる
  - 4. パースでreplaceするんじゃなく、構文解析の時点で+=1にする
    - 既存の文法が壊れた
      - Ruby++としてどうじゃろうか

## 構文解析と字句解析の違いについて教えて！

```
プログラミング言語のコンパイラやインタプリタでは、プログラムのソースコードを解析するために一般的に2つの主要なステップがあります：字句解析（lexical analysis）と構文解析（syntax analysis）。これらは、ともにソースコードを人間が理解できる形式からマシンが理解できる形式へと変換する役割を果たしますが、それぞれ異なる目的と役割を持っています。

字句解析：ソースコードは初め、一連の文字として存在します。字句解析（別名「レキシング」）の段階では、この文字のストリームをより意味のある単位、すなわち「トークン」に分割します。トークンは、キーワード、識別子、演算子、区切り記号、リテラル（数値や文字列など）といったプログラムの基本的な構成要素を表します。字句解析器（lexer）は、空白やコメントを除去する役割も果たします。

構文解析：字句解析によって生成されたトークンのストリームは、次に構文解析（別名「パーシング」）の段階に進みます。構文解析の目的は、トークンの順序と階層構造を確認し、プログラムの「構文」が正しいかどうかをチェックすることです。構文解析器（parser）は、トークンのストリームを受け取り、それを「構文木」または「パースツリー」（プログラムの構造を表現する木構造のデータ構造）に変換します。このツリーは、後続のコンパイラまたはインタプリタのフェーズ（意味解析、最適化、コード生成など）で使用されます。

したがって、字句解析と構文解析は、ソースコードを解析してマシンが実行可能な形式に変換するプロセスの異なるステップを表しています。字句解析はソースコードを意味のある単位（トークン）に分割し、構文解析はそのトークンを組み合わせてプログラムの構造を形成します。```
