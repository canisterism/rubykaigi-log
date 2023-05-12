# Ractor Recondsidered

- Ractorが使われてなくて悲しい
- そもそもRactorとは
  - Rubyアプリに並列性を提供する
  - オブジェクトがスレッドごとに独立するので、スレッドセーフなプログラミングができる（安全）
- なぜ使われてないのか
  - 使い方が難しい
  - ほぼ！独立したネームスペース
    - 例えば、Ractorの中で定義したクラスはRactorの外からは参照できない
    - ただし、クラス、モジュールなど一部のものは、Ractorの外からも参照できる
  - 古き良きActorスタイルのメッセージパッシング型のAPI
    - 例えば、Ractor#send, Ractor#receiveでお互いにメッセージパッシングする
  - エコシステムの問題  
    - 既存のgemがRactorに対応していない
      - 状態を変更してしまうっぽい?
  - 実装の問題？
    - 複数のRactorをRactor.selectで同期するのがむずい
    - パフォーマンス問題
      - 下手な実装をすると遅くなることさえある
      - GCの実行のために全部のRactorを止める必要がある
      - Ractorのスレッド作成はOSのネイティブスレッドを使うのでスケジューリングが難しい（？）
- 上記の問題から誰も使わない→FBがない→成長しないのバッドループ
  - なので実装クオリティとパフォーマンスを改善する（した）
  - M個のスレッドにN個のスレッドをマッピングする試みが始まった（MaNyProject）
- スケジューラの改善
  - Ring Example
    - Ractorを複数用意しておいて、乗り換えの際には次のRactorにメッセージパッシングする
    - これを環状に繋げることでRactorの生成コストを下げてるのか...？
- 複数のRactorでシェアされているオブジェクトがある問題
  - 分散GCで解決できそう
# メモ
- https://techlife.cookpad.com/entry/2020/12/26/131858
- https://www.wantedly.com/companies/wantedly/post_articles/430779