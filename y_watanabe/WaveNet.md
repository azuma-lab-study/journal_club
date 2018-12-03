
# WAVENET: A GENERATIVE MODEL FOR RAW AUDIO
(2016) Aaron van den Oord / Sander Dieleman (Google)  
https://arxiv.org/abs/1609.03499

## どんなもの?
- 生の音声信号を生成するネットワーク
- 従来より高速かつ高い性能
- 音声生成で人の主観的な自然さで評価してかなりの高得点
- 音声認識などにも使える

## 先行研究と比べて何がすごい？
- 客観的な自然さという意味で性能が高い
- RNN使ってないのでトレーニングが早い

## どうやって有効だと検証した?
- 公開されているデータセットを用いて自然さを複数の人の主観で判断した（MOS評価）
![image](https://user-images.githubusercontent.com/12442472/49049379-16cacf00-f222-11e8-972e-c110b0a19ebd.png)<br>
![image](https://user-images.githubusercontent.com/12442472/49049380-192d2900-f222-11e8-8f53-0df8024090cc.png)<br>

## 技術の手法や肝は？
- 受容野を広くするためのDilated Convolution
![image](https://user-images.githubusercontent.com/12442472/49049374-15010b80-f222-11e8-8460-b55092b4a735.png)<br>
- 音声生成の前提を組み込んだCausal Convolution
![image](https://user-images.githubusercontent.com/12442472/49049372-129eb180-f222-11e8-9820-66afb696d1d6.png)<br>

## 議論はある？
- 音声生成のみならずいろいろなタスクに使えそう

## 次に読むべき論文は？
- Gated Activationが音声全般に使えそうだったので超音波に使いたい
