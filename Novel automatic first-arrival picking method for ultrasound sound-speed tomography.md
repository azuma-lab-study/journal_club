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
        - 単純な系と複雑な胸部の形状を模擬した系とで精度検証した．
        ![image](https://user-images.githubusercontent.com/33616505/49047418-bd12d680-f21a-11e8-87fe-d0fffee94764.png)
## 議論はある？
ディスカッションで読んだものをここに書く

## 次に読むべき論文は？
参考文献で読んだものをここに書く
