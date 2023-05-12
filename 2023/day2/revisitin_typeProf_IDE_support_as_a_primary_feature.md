# Revisiting TypeProf - IDE support as a primary feature

>TypeProf is a type analyzer for Ruby code that has been bundled since Ruby 3.0. It has provided type inference of non-type-annotated Ruby code as a primary feature, and IDE support via Language Server as a secondary feature. This year, we are trying to reverse this; Let IDE a primary target. We're redesigning the analyzer to help achieving this. To speed up the response to edits in the IDE, we plan to make the analysis modular and incremental and reduce the amount of re-analysis per edit. We also plan to implement showing analyzed types as mouse hover hint by changing the analysis from bytecode-based to AST based. In this talk, we will present the new design of TypeProf and its prototype.

- typeprofとは
  - >TypeProfは、Rubyプログラムを型レベルで抽象的に実行するインタプリタです。 解析対象のプログラムを実行し、メソッドが受け取ったり返したりする型、インスタンス変数に代入される型を集めて出力します。 すべての値はオブジェクトそのものではなく、原則としてオブジェクトの所属するクラスに抽象化されます。
  - https://github.com/ruby/typeprof/blob/master/doc/doc.ja.md
