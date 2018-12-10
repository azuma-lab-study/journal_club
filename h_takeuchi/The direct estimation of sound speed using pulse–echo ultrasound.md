# The direct estimation of sound speed using pulse–echo ultrasound
1998, Martin E. Anderson and Gregg E. Trahey   
https://asa.scitation.org/doi/pdf/10.1121/1.423889?class=pdf

## どんなもの?
- 媒質中の縦波伝搬速度を直接推定する方法を提案．
- この推定方法には医用画像における,設定音速と環境音速の差異により生じるビームフォーミング誤差を動的に修正するといった応用可能性がある

## 先行研究と比べて何がすごい？
- 地震学における概念を参考に開発した，新しい手法である点．

## どうやって有効だと検証した?
- 均質媒質(液体)・不均質ファントムに対して音速推定を行い．精度が高いことを示した．  
- トランスデューサ
    - 素子数：128素子
    - 開口径：22.8 mm
    - サンプリング周波数：36 MHz
- パルス送受信回数：25回(走査線方向)
- 設定音速(送信フォーカス用)：1540 m/s
- ワイヤ
    - ワイヤ径： 94 μm
    - ワイヤ深さ：30 mm
![image](https://user-images.githubusercontent.com/33616505/49734723-95b31380-fcc8-11e8-82b9-9409276f5682.png)

## 技術の手法や肝は？
- ![2018_12_13_ 3](https://user-images.githubusercontent.com/33616505/49733988-4bc92e00-fcc6-11e8-8a0a-6512ccc17665.png)
![2018_12_13_ 4](https://user-images.githubusercontent.com/33616505/49733994-4e2b8800-fcc6-11e8-825e-7f05ce89d84f.png)

## 議論はある？
- 推定誤差の要因
    - 挙げられるもの
        - SN比
        - トランスデューサ形状
        - トランスデューサ位置決め精度
        - 媒質不均一性により生じる位相ずれ
    - シミュレーションを用いどの要因が大きく影響を与えているのかを調べた．
- 推定関数は波形の到達時刻・素子位置を含む．そのため，それら物理量に含まれる誤差により推定精度が低下する．
    - 相互相関法を用いるときに関係する，信号波形の時間軸方向の揺らぎ（ジッターエラー）
        - 原因：電気ノイズ，窓関数
    - 媒質不均一による位相収差
        - 不均一媒質における波形の空間相互相関は，Van Cittert–Zernike theoremによって説明できる．https://en.wikipedia.org/wiki/Van_Cittert%E2%80%93Zernike_theorem
        - 収差の要因は
        1. ビームフォーミング時の設定音速誤差
        2. 媒質不均一さによるランダムな位相誤差
    - 素子位置データの信頼性は，アレイの製造誤差によって低下する
![image](https://user-images.githubusercontent.com/33616505/49738819-ac129c80-fcd3-11e8-872e-2d3f780c21f1.png)
- fナンバー・定点フォーカス or 動的フォーカス・設定音速誤差による収差
![image](https://user-images.githubusercontent.com/33616505/49736552-d7928880-fccd-11e8-96d6-2969046a9094.png)
- future work
    - 音速分布推定の可能性に言及している．
## 次に読むべき論文は？
参考文献で読んだものをここに書く
- https://asa.scitation.org/doi/pdf/10.1121/1.5043402?class=pdf
    - 音速分布推定をこの論文の手法を拡張して行っている．
- https://asa.scitation.org/doi/pdf/10.1121/1.417973?class=pdf
    - 乳房の微小石灰化をこの論文の手法を応用して検出している．