
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
  
  
  
## DLによる再構成の理論的な問題
  - DL一般にメジャーなハードルはブラックボックス
  - 理論解析によってホワイトボックスにしようとしてる人もいるが、特定の逆問題に絞った研究は行われていない
  - 画像再構成に独特の問題は、
    - ネットワーク構成？（この理論研究は少ない、実験的な知見のみ）
    - どんな訓練方法であれば収束が保証されるか？（こっちの理論研究は多い）
  - CNNは研究されていて、Encoder-Devoderの構造は学習ベースのHankel行列分解によって表現される。
  - 数学だけでなく物理の概念もDLに貢献している
    - 対称性、局所性、複合性、多項式のLog確率は指数関数的に簡単なネットワークへ落とし込める
    - 
  - no-flattening theoremによればDNNは浅いNNでは正確に近似できないとされるが、多層のConicalな分解（ReLU）はどのような性質かまだわかっていない
  - 近年の研究によるとWell-designedなNNはよくない局所解を持たず、大域的最適解に行き着く
  - 今までの理論的研究の成果は、分類問題を対象としたシンプルなネットワークについて言及されたものが多い
  - イメージングにおいてこれまでの研究がどこまで適用できるかを考えることは重要な研究トピック
  - 
  

## Data-drivenなイメージングの研究領域
  1. Big Data Generation
  2. Image Domain Learning
  3. Data Domain Learning
  4. Hybrid Reconstruction Schemes
  5. End-to-End Workflows
  6. Convergence of deep imaging and other emerging technologies
  
  - ImageNetのタスクに比べて、CTなどのSinogramと再構成画像との写像は複雑なので、枚数はImageNetと同じかそれより多くないと無理そう
  - プライバシーとか法的な問題でImageNetほどの十分なデータは集められないので、過学習のリスク
  - 解決の可能性としては、転移学習やシミュレーションデータからの学習が期待される。
  
### Image Domain Learning
  - 主な課題：画質改善してるけど、本質的な処理なの？Cosmeticな処理なの？
  - YeがNNのアーキテクチャはWaveletのような信号の表現をしていることを数学的に示した（気になる）
  - 違いはその基底が学習により獲得されること
  - したがってImage Domainでのノイズ削減などの学習は本質的な処理を行っていると考えられる。（そうなのか？何回も畳み込むことは違うのでは？）
  - 
  
### Measurement Data Domain Learning
  - MRIのAUTOMAPがいい例（多様体近似の自動化？）
  - なんと一層目に全結合層を入れている
  - 
  - 
  
### MeasurementとImageの融合した情報を使った学習
  - 洗練された方法としては、NNを所望の函数空間への射影作用素として見ること
  - この時NNはFramelet信号表現と縮小の効果の両方を持つようになる
  - Iterativeになるので時間がかかってしまう欠点が生じる
  - 
  
  
### End-to-Endの学習
  - CTの生信号から肺の結節を検出する方法
  - 
  
  

## 次に読むべき論文は？
Deep Learning Computed Tomography、Wurfi
Chen, LEARN　Learned experts assessment-based reconstruction netwoek for sparse0data CT
AUTOMAP
Yeの画像ドメインの処理は数学的にWaveletと似たようなもんだ、みたいな主張の論文
Hankel行列って結局なんだったのか？（今の数学レベルだったらいけるかな。。。）



















