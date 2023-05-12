# Learn Ractor

- concurrencyはあらゆるところで起こっている
- 逐次実行は割と特殊ケース

- RubyでConcurrentはプロセスをフォークするけど、Ractorは新しいプロセスを作らない
  - オブジェクトのコピーを作らない（ので消費するメモリが少ない）
- Ractorはデータの隔離のために
  - Ractorは自信のブロックスコープ以外にはアクセスできない
  - 引数で渡せるんだけどコピーして渡せる（not参照渡し）
  - make_sharableで共有できるけどfreezeされる
- これらの制約が大変なので難しい
- じゃあどういうシチュエーションでハマる？
  - 数値の計算
  - インメモリDBへのアクセス
- ケーススタディ:ポケカ検索のための検索エンジン
  - デッキのアーキタイプに応じてクラスタリングする
  - 各週のRactorを作って計算する→都合のいいときに結果を取り出す（#takeする）
- iteratorで計算するような処理を見たらRactorの出番かも

- https://masaki.druby.work/city

# OpenMP

>OpenMP(Open Multi-Processing)とは共有メモリ型マシンで並列プログラミングを可能にする API(Application Programming Interface) で、FORTRAN、C/C++から利用できます。
