
# A Summary of DNN researches presented in IUS 2018

http://index.mirasmart.com/IUS2018/

## Concept
- ざっくりでいいので研究動向を知りたい
- IUSのDeep Learning系のセッションにおいてAbstract（本当に短い）の内容をまとめた


### Beamforming and speckle reduction using deep neural networks
Dongwoon Hyun, Leandra Brickson, Kevin Looby, Jeremy Dahl (Stanford Univ)
- やったこと  
  - スペックル低減のためにビームフォーミングでB-mode画像作るのにDNNを使ってみた
  - Focused channel signalsからB-mode画像作成
  - シミュレーションでデータ作成した実信号にも適用した
- 実験条件  
  - シミュレーションでトレーニング Field II で5000パターン作成
  - ネットワークはFully Convolutional Network 
  - Loss関数をUltrasound専用に設計し広いダイナミックレンジを確保
  - トレーニングはLoss関数、ネットワークの深さ、ネットワークの幅を変えて行った
- 検証方法
  - シミュレーションと実機でin-vivoデータ取得してhomgeneous部のSNRを算出、他の画像再構成手法としてDASやSpatial Compounding、Nonliner Meansと比較
- 結果
  - L2ノルムでDASと比較して94%エラー削減
  - Simulation, Phantom, in vivoにおいてSpeckle SNRはそれぞれ11.0, 7.7, 3.1だった
- 結論
  - DNNを用いた提案手法はDAS, CS, NLMより高い性能を発揮した
  - シミュレーションによる訓練によってin vivoの条件においても汎化できることが示された。
  - Verasonics使ってリアルタイム実装できた。


- コメント（渡部）
  - FCNはU-Netの進化版、2016年のセグメンテーション用のモデルだったと思うので新しいモデルにする方向もあるかも？
  自分もU-Net使ってたけど、セグメンテーション用のモデル使うのはどうなのかと思っていたけど、この人たちはそこに関して疑念は無いのだろうか。
  - シミュレーションからin vivoの条件に対して汎化できることを示したのはすごい。
  - 詳細書いてないからよくわからんけどこの場合のビームフォーミングというのは各素子の波形をSUMするときに代わりにDNNを通して綺麗にするってこと？
  - 色々なパターン試したらよくわからんところで変な挙動するってことはよくあるけど、この場合はどうなのだろう？
  - ↑よく考えたら手動の撮像だとちゃんと当てないとDNNへの学習データにないもの（Out-of-Distribution）を入力することになって、変な挙動しそう。
  その点リングアレイなら手技に依存無しなので相性よいのでは？
  
  
  
  
### Reverberation Noise Suppression in the Aperture Domain Using 3D Fully Convolutional Neural Networks
Leandra Brickson, Dongwoon Hyun, Jeremy Dahl (Stanford Univ)
- やったこと  
  - 層構造の組織からの多重反射により生じるノイズ（Reverberation noise）と、熱雑音を取り除くフィルタを3DCNNで構成
  - シミュレーションでデータ作成した実信号にも適用した
- 実験条件  
  - シミュレーションでトレーニング Field II で5000パターン作成
  - Field IIはImpulse応答を使っていて波動伝搬過程を考慮できないので多重反射成分はノイズなしシミュレーションにバンドパスフィルタ（意味？）
  をかけて作成、足し合わせて多重反射付きRFデータを作成した
  - 熱雑音（-20 dB to 10 dB）
  - ネットワークの入力は復調後の遅延させたRF信号である
  
- 検証方法
  - シミュレーションと実機でin-vivoデータ取得して再構成画像、波形の相関、CNRで評価
- 結果
  - 復元した波形の見た目はchannel方向に平滑化されたようになっていた、ノイズなしの物とよく似ている
  - ノイズの多いデータの場合正規化相互相関は0.69から0.92へ増加した
  - CNRは病変部分で1.12から1.23へ増加した
- 結論
  - 3DCNNで多重反射ノイズの抑制ができた

- コメント（渡部）
  - ネットワークどうなってるのか
  - Channel方向に平滑化されたというのはポジティブな意味？
  - Reverberation Noiseって一般的な用語っぽいけどあんまり分かった感ない
  - 多重反射完全に再現できてるの？よくわからない
  - なんで多重反射信号作るときバンドパスかけてるの？周波数帯で被るようなノイズ無くない？
  - 結果はin vivoデータ？
  - 自分の研究について、Field IIで訓練してうまくいくなら時間のかかるk-waveでやる必要もない？
  - もしくはK-waveでしかできないことを研究テーマにするか。骨の多重反射とかはそれっぽいなと思う
  
  
### Evaluating the Robustness of Ultrasound Beamforming with Deep Neural Networks
Adam Luchies, Brett Byram (Vanderbilt Univ)
- やったこと
  - ビームフォーミングのタスクで電気的ノイズ、（バルクの）音速不均一、位相収差をDNNで補正
  - シミュレーションデータだけで実際のアプリケーションに適用できるか調べた
  - B-mode上のClutterノイズを減らすために昔から研究してて、ADMIREという手法を開発してた
  - ADMIREの主張するところとしてはビームフォーミングは非線形回帰問題に落とせるということ
  - DNNで非線形回帰を行う、というつもり

- 実験条件  
  - 訓練は1-3個のポイントターゲット（散乱源？）に対してoff-axis scatteringのみを抑制するように行った
  - そのときにSNRを変えたり音速不均一、無エコー嚢胞による位相収差を作った。これを抑制するようには明示的に訓練していない
  
- 検証方法
  - シミュレーションで訓練してin vivoの肝臓でテスト
  - CNRで比較
- 結果
  - DASに比べてCNRが4.3 dBから5.0 dBに改善した
- 結論
- DNNは頑健だと結論付けた（ん？）

- コメント（渡部）
  - 実験条件がよくわからない
  - 数学的な手法だとこういう問題になるのでDNNもこれを解くことになっている～的な論法のパターンだけど、本当にその問題を解いていることになっているのか？
  - アブストなのでわからないところもあるが、頑健だと結論付けた根拠が知りたい（多分この領域で一番重要）
  - データ作成条件がよくわからない
  
  

