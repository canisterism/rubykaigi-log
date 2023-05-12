# Multiverse-Ruby

https://github.com/shioyama/im

- Rubyはネームスペースが共通なので、クラス名が重複すると上書きされてしまう。
  - →Portableではない
  - これをどないかして解決する
- 思い出すシリーズ: Rubyのmoduleによる名前空間の違い

```ruby
# 名前付きmodule
module Mod
  def self.hoge
    1
  end
end
```

```ruby
# 匿名module
mod = Module.new
mod.hoge = 1
```


- 匿名moduleを使って、名前空間を分ける
- permanent rootにはObjectがいる
  - Fooとかの定数を定義すると実はObject::Fooという定数が定義されている
- 同じようにして、匿名moduleをpermanent rootに定義し、各gemでそのmoduleのnamespaceを使うことで名前空間を汚染しないようにする
- Ruby3.2で入った `load` メソッドに第2引数を渡すとそのnamespaceでロードされる
  - requireをloadで置き換えるのは難しい
  - 依存先も全部書き換えないといけない
- Zeitwerkのforkとして https://github.com/shioyama/im を作った
  - そもそも：Zeitwerkとは
    - Railsのautoloadを高速化するgem
    - hoge/fuga/bar.rb → Hoge::Fuga::Barというクラスを定義する
- これを使うと、gemの名前空間を汚染しないようにできる
  - また、自前のアプリケーション内の名前空間内でgemをrequireすることで他のnamespaceとの名前空間の衝突を防ぐことができる
