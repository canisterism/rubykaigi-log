# Power up your REPL life with types

>Nowadays, we can use the power of types when writing code in an editor or IDE. But how about in IRB? What if the auto completion of IRB gets more accurate using type information? Wouldn’t it be happy? In this talk, I will show how to implement type based auto completion and make your own customized IRB.

- IRBの自動補完はメソッドチェーンすると動かない
  - https://github.com/tompng/katakata_irb で動く
- IRBの実装について
  - Reline
    - Multilineの入力を受け付けるEditor
  - IRB
    - REPLの実装
- 候補を出すためには正規表現を使っていた
  - `[]`ならArrayみたいな
- これだと不安定なのでRubyのパーサを使うことにしたっぽい
- 1.S式で与えられた式をAST的な感じにできる？
- 2.次に、与えられた式のレシーバの型を判断する
  - RBSの型が1で分かってるのでパターンマッチで作れる
- 3.補完を出すための仕組み
  - 新しいREPLのセッションを作る（厳密にはcompletion_proc.callに新しいセッションを作って突っ込む）
- もっと補完したい
  - break, next, returnなどの制御構文が絡むと難しい
  - ありえる型のUnionとして解決してるっぽい？

# メモ

## S式って？

S式（S-expression）は、LISPプログラミング言語やその派生言語で使用されるデータ表現形式の一つです。"S"は"Symbolic"を指し、S式はシンボリックな表現方式です。

S式はリスト構造を持ち、一般的には括弧で囲まれた項目のリストとして表現されます。例えば、(add 1 2)というS式は、"add"というシンボルと、数値の1と2という3つの項目からなるリストを表現しています。

S式はデータとコードの双方を表現することができ、これがLISPの「コードはデータ、データはコード」（code is data, data is code）という哲学の基礎となっています。これにより、LISPではプログラムが自分自身を操作・変形するメタプログラミングが容易になります。

また、S式は木構造を自然に表現できるため、構文解析が容易であり、プログラミング言語の設計やインタプリタ、コンパイラの実装において有用です。
