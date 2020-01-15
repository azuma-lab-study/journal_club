
# Image Reconstruction Is a New Frontier of Machine Learning
(2019) Ge Wang, et.al. 
https://ieeexplore.ieee.org/document/8359079


## どんなもの?
- 概要
  - CNNのConvolutionを周波数空間で行うようなネットワークを構築
  - Classificationタスクの実行時間を比べたら大きな画像サイズでは提案手法のほうが最大40倍高速だった

- イントロ
  - Medical Imagingでは画像再構成と画像解析が２本の柱、この論文は画像再構成について
  - 画像解析については”Deep learning in medical imaging”が相補的な姉妹編なのでそっちも見ると良い
  - 従来の解析的な方法とIterativeな方法に加えてMachineLearningでの画像再構成は新しい方法となる
  - ２０本のそれぞれ３−４人によってレビューされた、機械学習特にニューラルネットワークを用いた論文についてまとめた
  - 普通は以下のパイプライン
    - (1)forward projection, backprojection and/or regularizationとしての画像再構成
    - (2)ノイズ・アーチファクト除去などのポストプロセシング
  - 紹介するいくつかの論文では、低S/N, 少ない情報、限られた角度、スパースな情報取得、対象の状態によって生じるアーチファクトを克服するためにMLを使った
  - X線CT,MRI, PET、光音響など
  - Adlerの方法のような、モデルベースの再構成オペレータをDLと統合したもの、
  - Chenのスパースコーディングを拡張子正則化パラメータを学習、パラメータがイテレーション依存の形式であるもの
  - WurfiのCone-beam CT再構成におけるCorrection matrixの重みの学習
  - ZhengのLow-doseCTにおけるペナルティ付き最小二乗法を用いた変換の学習（？）
  - GuptaのCNNを用いたProjected Gradient Decsentは、スパースなCTの問題に適用された。
  - ShenはTV法で行うCT再構成のパラメータチューニングに深層強化学習を利用した。
  - ZhangはスパースビューCTにおけるDenseNetとでDeconvolutionを用いた画像再構成
  - HanはFraming U-net使ってCT再構成
  - ZhangはX線CTの金属によるアーチファクトの低減にアンサンブル学習を使った
  - ShanはConveying path based encoder-decoderを使ってCTのデノイジングを行なった。
（特徴は２Dで学習させたDonoisingを３DにFine-tuningできるところらしい） 
  - 以上は画像再構成にNN使ったやつ。以下はCompressed sensingフレームワークにDNN使ったやつ。
  - QuanはGANにCyclic lossを使ってMRIでCSさせた。（おそらくCSのIterativeな計算部分にGANを利用した？）
  - GozcuはMRIの最適なサンプリングパターンにDNN使った。（これ面白そう。USにも利用できそう）
  - KimはPETの画像再構成にペナルティ付きのDLを使ったDenoisingステップをを従来のIterativeな計算の前に組み込んだ。（気になる）
  - YangはBaysianのPET再構成にDNN使った。（気になる）
  - Allmanは光音響におけるニードルやカテーテルが作るアーチファクトの低減にDNNを利用した。
  - Hauptmanはモデルベースの学習を使ってLimited-viewからの３D画像再構成を行なった。
  - 

## 先行研究と比べて何がすごい？
- Fourier領域で処理することでConvolutionを高速化する研究はあるが、処理中で空間領域とFourier領域を行き来するため無駄が生じている
- またその他の先行研究でFourier領域でダウンサンプリングすることで空間情報をなるべく保持したまま収束性を向上させる手法が提案されている
- 提案手法では処理前にFourier変換を施し、逆フーリエ変換はしないまま処理を最後まで行う


## どうやって有効だと検証した?
- 概要
  - 単純〜複雑なデータセットでAccuracyと速度を比較
  - ネットワークの層数は同じにした
  - MNIST (28 x 28のグレースケール画像、10 Class分類問題)
  - Cifar-10 (32 x 32のRGB画像、10 Class分類問題)
  - Kaggleの超音波画像データセット（元画像をダウンサンプリング、5 Class分類問題）
- ネットワークについて
  - 処理がシンプルなのでAlexNetをベースに選択（渡部：今はResNetが性能良いとされているが、あえてAlexNetを選んでいると思われる）
  - Convolution Kernelは周波数領域で表現、PoolingはFourier領域で間引くことで代用（異なる処理になるが十分動く）  
  ![image](https://user-images.githubusercontent.com/12442472/48743260-b24dc400-eca5-11e8-8c6c-d4835a4e0757.png)  
  ![image](https://user-images.githubusercontent.com/12442472/48743282-cee9fc00-eca5-11e8-8a87-6b1c4563a63b.png)  
  - DropoutとDense結合はそのままFourier領域で実装
  - バックエンドをTheanoにしてKerasで実装
  - FFTの層はTheanoで実装
- 実験結果
![image](https://user-images.githubusercontent.com/12442472/48743331-022c8b00-eca6-11e8-9582-e9cdc63dda64.png)  
![image](https://user-images.githubusercontent.com/12442472/48743350-1a040f00-eca6-11e8-8de4-c16284c4c8a3.png)  
  - MNISTはAccuracy下がった、Cifar-10では上がった
  - 処理速度は画像サイズによるが小さい場合は同じ速さ、画像サイズに対して指数関数的に差がつく



## 技術の手法や肝は？
- 空間領域でのConvolutionはFourier領域でのHadamard Production（要素ごとの積）になるので計算コストが低くなる
- FFTとIFFTを行き来しないのでコスト削減になった
- 空間領域のKernelとくらべて周波数領域のKernelは自由度が大きいので表現力UP
- (渡部) ↑それはそうだけどパラメータ数増えるからメモリ圧迫しない？大きなモデルだと弱点になるのでは？


## 議論はある？
- MNISTで精度落ちてるのは画像サイズが小さすぎてFFTするときに情報が欠損するから
- Cifar-10ではFCNNがAccuracy上回った、これはKernelがFourier空間だと表現力が増すから
- (渡部) ↑それはパラメータ数が増えたからでは？同じ層数で比較するのも良いけど、同じパラメータ数で比較したらどうなる？
- ネットワークのアーキテクチャに依存せず使えるので、いろいろなタスクで使われると良い
- (渡部) 空間CNNでKernelサイズが大きいと深い層での受容野が大きくなるので画像の文脈を考慮しやすいとの論文を見たことがあるが、
このFCNNは空間領域のKernelサイズは実質任意ということになるので文脈を考慮した処理ができるのではないか？

## 次に読むべき論文は？
Deep Learning Computed Tomography、Wurfi
Chen, LEARN　Learned experts assessment-based reconstruction netwoek for sparse0data CT



















