# Novel automatic first-arrival picking method for ultrasound sound-speed tomography
2015 Xiaolei Qu, Takashi Azuma  
http://iopscience.iop.org/article/10.7567/JJAP.54.07HF10/pdf

## どんなもの?
- USST(Ultrasound sound-speed tomography)の取得画像品質はTTM(travel time map)の精度に依存している．
- そこで，本研究では自動的に信号最短到達時刻をもとめる新手法を開発した．  
  1. 赤池情報量基準(AIC)
  2. 相互相関  
  これら2つを参考にして「赤池情報量基準・隣接相互相関法」を開発した．
## 先行研究と比べて何がすごい？
- 精度良く信号最短到達時刻をもとめた点．
## どうやって有効だと検証した?
- シミュレーション・ファントム・ex vivoで実験を行った．
- シミュレーションによる結果では，単純な系・複雑な系でそれぞれ絶対推定誤差は52 ns, 98 nsであった．
- ファントム・ex vivo実験によって，提案手法の実現可能性を示した．

## 技術の手法や肝は？
- 従来手法
    - 相互相関法(cross correlation)  
    ![image](https://user-images.githubusercontent.com/33616505/49046300-f8aba180-f216-11e8-8f89-24547874d919.png)
    ![image](https://user-images.githubusercontent.com/33616505/49046315-07925400-f217-11e8-86e1-f322f0cd80fc.png)
    - AIC法  
    ![image](https://user-images.githubusercontent.com/33616505/49046391-4fb17680-f217-11e8-982c-5488db26c787.png)
- 提案手法
    - AICNCC法(AIC & neighbor cross correlation)  
        - 隣接する素子同士のRFデータは似ているという性質を利用した点が肝．
    ![image](https://user-images.githubusercontent.com/33616505/49046642-23e2c080-f218-11e8-808e-4f7d9b60c73f.png)
    ![image](https://user-images.githubusercontent.com/33616505/49046715-61474e00-f218-11e8-8b0b-e969596a6f40.png)
- シミュレーション・実験手法
    - 商用ソフトウェアを使ってシミュレーションを行った(PZFlex)
        - 音速分布再構成にはbent-rayに基づいた再構成法を用いた
            - 一般的な投影法(逐次近似投影法)
                - 入力：組織の音速分布
                - 出力：受信信号  
                1. 入力は仮定され，出力は計算される．
                2. 計算された出力と実際の出力との差を比較
                3. 出力の差をなくすように入力データを逐次修正する
                4. 1以降を繰り返す
            - bent-rayに基づいた投影法
                1. bent-ray tracing
                2. 同時代数再構成法(SART; Simultaneous Algebraic Reconstruction Technique)による逐次逆投影再構成
            - bent-ray tracingの原理
                - フェルマーの原理に基づく．  
                ![image](https://user-images.githubusercontent.com/33616505/49048085-dd439500-f21c-11e8-9012-d3b50d89429e.png)
        - 256素子のリングアレイトランスデューサ
        - リング直径は100 mm
        - 素子サイズは1.23 mm
            - 素子内には81個の点音源が並んでいる
        - 中心周波数は1 MHz
        - サンプリング周波数は10 MHz
        - 単純な系と複雑な胸部の形状を模擬した系とで精度検証した．
        ![image](https://user-images.githubusercontent.com/33616505/49047418-bd12d680-f21a-11e8-87fe-d0fffee94764.png)
    - 超音波CTのプロトタイプでファントム・ex vivo実験を行った
        - 1024素子中の256素子を用いた
        - 中心周波数は2 MHz
        - サンプリング周波数は10 MHz
        - リング直径は100 mm
        - ファントム実験
            - シミュレーションと対応させるように，単純な系と胸部の形状を模擬した系とでデータを取得した  
        ![image](https://user-images.githubusercontent.com/33616505/49048597-aa9a9c00-f21e-11e8-800f-87188d53f18c.png)
        - ex vivo実験
            - 鶏の肉片：小サイズ・大サイズの二種類  
            ![image](https://user-images.githubusercontent.com/33616505/49048704-0d8c3300-f21f-11e8-95c6-a5396c7d3f5b.png)
## 議論はある？
- 結果
    - シミュレーション  
        - ノイズなしだと，AICとAICNCC両者とも検出誤差がほぼ見られない
        - ノイズありだと，AICの検出誤差が大きくなっていることが確認された  
    ![image](https://user-images.githubusercontent.com/33616505/49048796-75db1480-f21f-11e8-8bdb-5c282b59bcf6.png)
    ![image](https://user-images.githubusercontent.com/33616505/49048895-f4d04d00-f21f-11e8-8bc7-ec2200093ffa.png)
    ![image](https://user-images.githubusercontent.com/33616505/49048955-3c56d900-f220-11e8-9a67-948ff0eb1c2d.png)
    ![image](https://user-images.githubusercontent.com/33616505/49048999-80e27480-f220-11e8-8a82-8913568f1a40.png)
    - ファントム実験
        - AICNCCで再構成した
        - 内部構造が確認できた  
        - They could show the internal structures of both phantoms because our proposed AICNCC method worked well.
        -  Furthermore, the sound speeds in both the simple circle and complex breast phantoms in the reconstructed images were 1457 ± 6 and 1417 ± 14m=s, respectively.
        - Compared with their measured sound speeds (gold standards), which were 1452 ± 3 and 1393 ± 4m=s, the reconstructed simple circle image showed a slightly better accuracy.
    ![image](https://user-images.githubusercontent.com/33616505/49049098-e9315600-f220-11e8-85ea-d178716e0390.png)
    - ex vivo実験
        - Furthermore, the sound speeds in chicken breast meat in the reconstructed images were 1557 ± 18 and 1564 ± 19m=s for the small and large meat specimens,
        - which were close to the measured sound speed (gold standard) of 1572 ± 3m=s.  
    ![image](https://user-images.githubusercontent.com/33616505/49049246-94420f80-f221-11e8-98d9-962f318e1d0d.png)
- 議論
    - AICやCCと比べてAICNCCは構造の複雑性やランダムなノイズに対して頑健性があるといえる
    - CCはノイズに対して非常に頑健性があるが，構造が複雑になると精度が悪くなる
    - AICは構造の複雑性に対して頑健性があるが，SN比が悪くなると精度が悪くなる
    - ランダムなノイズを除去することで更に精度が上がる．
        1. 複数のRFデータを平均化すること
            - 信号取得回数が増えるので時間が更にかかってしまう．
        2. バンドパスフィルタをかけること
            - とても良い方法なので使いたい．  
        ![image](https://user-images.githubusercontent.com/33616505/49049663-5219cd80-f223-11e8-99dc-008baca7b65b.png)
        ![image](https://user-images.githubusercontent.com/33616505/49049671-5e058f80-f223-11e8-84d5-90c9e9802d14.png)
            - 適用してAIC法の精度を上げたが，AICNCC法のほうが精度が高い．
## 次に読むべき論文は？
参考文献で読んだものをここに書く
