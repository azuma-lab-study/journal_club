
# Ultrasound Computed Tomography: Historically Guided Musings
(2017) James.F.Greenleaf (Mayo Clinic College of Medicine)  
https://publikationen.bibliothek.kit.edu/1000071328

## どんなもの?
- Review的な論文
- USCTの発明者のGreenleafがUSCTの今までの議論とこれからの進化の方向を解説  
- 今後の方向性にはAIによる解析とある。（渡部：AI超音波の研究はホットっぽい。USCT系でも次回の学会は多いのかもしれない。）  

![image](https://user-images.githubusercontent.com/12442472/49741260-61941e80-fcd9-11e8-81a8-6fea3b2d86e5.png)  

## USCTの今まで

- 研究の流れについて
  - 乳房の腫瘍を描出することに研究は集中してきた
  - コンピュータのマシンパワーのおかげでWave Propagationの複雑な数学モデルの逆問題も解けるようになった
  - USはそもそも非侵襲で安い
  - 加えて数学的に複雑な演算が必要ない断層撮像方法→ 診断におけるEarlyな段階で使われるように
  - Greenleafが発明
  - Gloverが最初のin vivo実験
  - Carsinが患者の軟組織を撮像
  - MacDonnellが心筋梗塞における減衰メカニズムをUSCTで研究
  - USCTは360°をカバーする複数の複数の方向から撮像することが必要
  - 15%の米女性がCacinoma（上皮細胞で起こる癌）になる, もっと多くがcarcinomaと弁別されるべき疾患を持つようになる
  - →乳房が研究対象になった

- よく使われるモデルについて  

  ![image](https://user-images.githubusercontent.com/12442472/49742384-ca7c9600-fcdb-11e8-80a3-ee6e602bbd82.png)  
  ![image](https://user-images.githubusercontent.com/12442472/49742417-dc5e3900-fcdb-11e8-9d6c-2fbf62d09e3b.png)  
    
  
  - aは送信素子の位置、bは受信素子の位置、Aは振幅、dsはaとbを結ぶ反射波の直線経路、Tは到達時間、Nは屈折率、NRはNの実部、NIはNの虚部（減衰係数）
  - これらは直線の経路を想定、組織間のNの変動が小さいときすなわちNの二次以降の項が無視できるとき使える
  - もっと正確なモデルはMueller, Kaveh, Stenger, Johnsonが作った方法を使うべし
  - 1977年には音速不均一による収差の影響をBmode像から補正する方法を使って乳がんをUSCTで診断した
  - 同じころMuellerとDuckは定量的なBackscaterのTomographyを開発した（渡部：よくわからない）

- 実際にとれる画像
  - 1970年前半に撮像された乳房、音速と減衰で腫瘍が分かる
  - 腫瘍は高いあるいは低い減衰を持つが音速は大体高い  
  ![image](https://user-images.githubusercontent.com/12442472/49743246-a8841300-fcdd-11e8-8e20-c8c7f99300f1.png)  

  - 音速と減衰の重畳した画像
  - 音速の高いところが腫瘍で、若い人では高減衰の実質部で囲まれ、高齢の場合は高減衰で縁取られるか合同な形の減衰が出る
  
  ![image](https://user-images.githubusercontent.com/12442472/49743265-b0dc4e00-fcdd-11e8-8803-8403d5862baf.png)  

## USCTのこれから
- もう商用のものが臨床試験やっててそろそろ世に出そう
- Wave Propagation解くのはできるようになってきたけど、データの取得方法が問題で360°とらなきゃいけない（渡部：3D伝搬結果の取得方法のこと言ってるの？）
- なにかブレークスルーが欲しいが、AIがいいかも
- AI超音波はもう研究され始めていて、インパルス応答をAIで改善する研究などがある（渡部：ここで取り上げるくらいなので気になる）
- USCTのアルゴリズムに適用できるかはわからないけど可能性はある
- データ（渡部：RF信号のこと？）と画像のどちらに適用するかはわからない
- 計算パワーとAIの２つの発達が医療分野で重要なツールとなる。

## コメント
- 論文書く時の引用で、乳房しか研究されてませんよとかDNN期待されてますよっていう部分で使えそう
- もうちょっとBmodeの性能面に言及してる論文が読みたい

## 次に読むべき論文は？
- AIの超音波応用で引用されてたやつ  
A. Luchies, B Byram, Deep neural networks for ultrasound beamforming,
Proceedings of the Ultrasonics Symposium, 2017
http://ieeexplore.ieee.org/document/8092159/ 
- あとは論文にかけるように主要なUSCTの論文に目を通しておきたい。




