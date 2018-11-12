
# DEEP LEARNING FOR ACCELERATED ULTRASOUND IMAGING
(2017.10) Yeo Hun Yoon / Jong Chul Ye 
https://arxiv.org/pdf/1710.10006.pdf

## どんなもの?
- ポータブル超音波診断装置や3D超音波イメージング、超高速イメージングなどの新しい領域では、得られるRFデータが少ない。  
- しかしながらRF信号は周波数空間でSparseであり、冗長性を持っている。  
- Sparse性を利用したアプローチに圧縮センシングを用いた手法があり、少ないRFデータから解像度を落とさずに画像再構成できることが示されているが、逐次解法を用いるため計算コストが大きい。  
- Deep Learningによる演算は一般に高速であるから、少ないデータからRFデータを補完する手法を提案した。  
- サブサンプリングされたRF信号から補完されたRF信号によって得られた再構成画像は、すべてのRF信号を使ったものとほとんど変わらない結果を得た。

## 先行研究と比べて何がすごい？
- 圧縮センシングを用いた手法や、Hankel Matrixを用いた補完手法はデータを正確に再構成できるが、高計算コスト。
- 提案手法は計算速度が高速であり、さらにその性能は対象に依らず普遍的な性質を持つ。
- 実験的には、コンベックスプローブで訓練したネットワークを使用してリニアプローブで得られた信号に適用しても正確な処理ができている。

## どうやって有効だと検証した?
- リニアプローブ（中心周波数 ： 8.48 MHz）、サンプリング周波数40 MHz  
- 訓練は実機で取得した7人のデータから15000個のRx-SCデータを訓練に、別の１人から3000個のRx-SCデータをValidation,もう1人をTestセットにした。  
- 入力は1/4にダウンサンプリングされたRFデータ（受信素子方向）  
- ネットワークはU-NetライクなCNN + Concatenateの構造  
- OptimizerはSGDで正則化パラメータは$10^-4$、400 Epoch回した  
- 　学習率は$10^-7$から$10^-9$まで段階的に下げた  
- 復元したRF信号を用いてDASで再構成した画像で比較  
![image](https://user-images.githubusercontent.com/12442472/48365943-b733d600-e6ef-11e8-88b4-5d15afa1e67e.png)  
![image](https://user-images.githubusercontent.com/12442472/48365947-b9963000-e6ef-11e8-8bc3-c69657f3cfc4.png)  
- Convexプローブ（中心周波数 : 3.2 MHz）にも適用し検証  
- 定量的な評価はPSNR（Peak Singal to Noise Ratio）で行われ、画像ごとの平均では約30.92 dBで、サブサンプリングRF信号を用いた場合に比べ約10 dB改善した。  
  
## 技術の手法や肝は？
![image](https://user-images.githubusercontent.com/12442472/48365795-3f65ab80-e6ef-11e8-96e6-9551c80d5530.png)  
![image](https://user-images.githubusercontent.com/12442472/48365799-42609c00-e6ef-11e8-9cd3-255ef430dbc4.png)  
![image](https://user-images.githubusercontent.com/12442472/48365746-1fce8300-e6ef-11e8-9b81-b735843c4132.png)  
- 肝としては、適当にDeep Learningを適用しましたという話ではなく、
数学的にSparse性があるとわかっており少なくともHankel Matrixを用いた手法などでは少ないデータから冗長性を利用して有用な情報を抽出できることが示されていること。  
- データの大量取得という意味では、教師データはRF信号と、そこからサブサンプリングしたRF信号だけで良いという設定が有利だと感じられる。臨床データをとれば質の問題も無い。  
- （渡部）ネットワークに関しては適当に感じる。とくにそこに肝は無さそう。
- （渡部）入力データは正規化してるのか？　ならば、SGDで学習率を変えていく所は参考にできそう。Lossは不明。

## 議論はある？
- リニアで訓練→ コンベックスに適用してもできたので普遍性があると言える  
- （渡部）周波数違ってもできるというのが驚き。  


## 次に読むべき論文は？
- Hankel　MatrixによるRF信号の冗長性の説明を詳しくみたいので、↓  
- [3] Jong Chul Ye, Jong Min Kim, Kyong Hwan Jin, and Kiryung Lee, “Compressive sampling using annihilating filter-based low-rank interpolation,” IEEE Transactions on Information Theory, vol. 63, no. 2, pp. 777–801, Feb. 2017.  

