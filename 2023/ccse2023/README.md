## CCSE2023
主にサイバーエージェントAI Labのメンバーが中心となって運営されている、企業研究にフォーカスしたカンファレンス。
大体１年に１回開催、しばらくコロナで開催していなかったが、久々にオフラインで開催。場所は東大。参加費１０００円で、特定の学会に所属しなくても誰でも参加できる。
お弁当もでる！ありがたき。参加者は基本的にはスポンサー企業のメンバー、大学生、その他の企業のそれ漢検の人、あと一般の人もOK.

今回は朝から１日参加。

以下見た、公演の感想などを記載。私の興味関心範囲は以下のところへん

* LLM, NLP
* MLOps
* ロボティクス
* 量子コンピュータ

### 大規模言語モデルのMerge技術の検証 (NLP)
* 石上 亮介
* 株式会社サイバーエージェント

なんかLLMのマージ技術（結合）っていうのがあるらしい。

`AというタスクでファインチューニングしたモデルA`と, 
`BというタスクででファインチューニングしたモデルB`

をマージすることで、A、Bのタスクが両方に対応した（オリジナル精度よりは落ちる）モデルを作成することができるらしい。

マージ方法は、モデルの重みを平均したり、transformer層を上下にスタックしてつなげるなどの方法（結構いろいろけんきゅうされている）みたいなのができるらしい。
単純に性能の和だけではなく、差分マージもできるらしい。なつーか幾何学的な操作ができるらしい。マジデカ？

差分マージはこんなん

英語の基盤モデル に インストラクション学習して 英語(インストラクション)ができる。
英語(インストラクション)モデルから元の英語基盤モデルの部分を引く、そうするとインストラクション部分だけが残る。
このインストラクションを、日本語の基盤モデルにひっけてやると、英語のインストラクションデータで学習した、日本語のインストラクションモデルができるらしい。（もちろん最初か日本語、日本語インストラクションデータで学習しがほうが性能はよいとは思うが）


## 日本語事前学習モデルの公開とその意義 (NLP)
* 沢田 慶 さん
* rinna株式会

**あとで個人的に質問をしにいってお話を伺ったで下記にはその情報につても公演情報にプラスされています。**

講演者はrinnaの研究チームのリーダーの方。最近のrinna社のオープンソースへの寄与についてご紹介されていた。
基本的にこの分野の人は昨今のrinna社のオープンソースへの寄与率の高さは知っているので特段説明はいらないだろうが、
やっぱりキャラクターチャットボットのビジネスがメインっぽいのだが、どいうビジネスモデルなのかは正直未だに不明である。

いろいろな種類のモデルをオープンソースとして常に新しいモデルを提供しているのが驚き。いつもrinnaにはやられてっぱなしであると言ったた当人は自慢げそうだった。
すくなくとも、上記の施策のためにGPUリソース（金）がかかるのだが、どっから金がでていのかはやはりマイクロソフトからなにかしら支援があるのではないかという感じ。

そのあたりについてはカマかけて計算機環境について聞いたら、Azureの環境についてはオンデマンドではなくプリザーブ枠が一定数あるのでそれを利用しているとのこと。あとAWSのLLM 開発支援プログラムにも採用されているので、そういう活動の結果だとのこと。一応、オープンソース活動の延長線でお客様がくることもあるとのこと。

あと、昨今のオープンソースの頑張りすぎているが、なぜそういうことができているのかと聞いたら、社員で１名よくできるのがいるので、その人が爆速でやっているとのこと。
基本的に`Stability AI`の人も行っていたけど、、モデルのリリースのタイミングとかは、リーダーボードで１位になれるかどうかが結構バイアスとしては大きいとのこと。今出せば、リーダーボード１位になれてうれしい、みたいなそういう無邪気な動機も結構あるようだ。

## Contract One における契約書解析技術の開発 (NLP)
* 保坂 大樹　さん
* Sansan株式会社

Sansanの契約書解析プロダクトに関するノウハウなどの共有、[Contract One](https://contract-one.com/) のプロダクトは契約書情報のDB化をするらしい。
LLM関連ではLLMで契約書の要約を実施しているみたい。要約の精度やハルシネーションについて質問されていたけど、UIでカバーしているとのこと。
要約文の隣は原本を表示するようになって、最終的には自分で確認してねという話のようだ。

## 大規模言語モデルのZero-shot Learningを用いたデータ構築と開発への応用 (NLP)
* 大嶋 悠司　さん
* 株式会社メルカリ

講演者はメルカリのLLM(生成系AI)のテックリードの人。
メルカリでLLMをどのように活用しているのかの事例紹介。基本的に基盤モデルやファインチューニングモデルを整備していくという基盤よりのタスクではなく市中のLLMをどいうメルカリのサービスに導入して、お客さんに付加価値、社内メンバーには作業の効率化などを提供していくのかがミッションみたい。社内向けと、お客さん向けに２つのLLMの応用の事例を紹介されていた。ここでzero-shot というのはいわゆるRAGのことである。ファインチューニングなしの素のLLM（たぶん言及してなかったけど、１００％ OpenAPI のchatgptシリーズを利用を想定）をzero-shotとういかRAGをつかってどのように利用するかについて。

 * 社内向け (SQLの作成支援)  
 これままさにLLLMのパワープレイという感じで社内のDS(データ・サイエンティスト）はSQL書くのめんどうだぜー。１日に何個もつくってられねー。というんでLLMで社内DBを検索するSQLを作ってやろうずというアプローチ。ただしDBのテーブル構造とかも暗黙知でコメントがないテーブルなども多いのなにがなにやらわからん。
 あので、SQLのクエリログをまずはLLMに打ち込んでテーブルの構造をLLMの予想させて、その予想値テーブル情報をもう一度、LLMに食わせてあるタスクを実行するSQLをその情報を元にSQLを生成させてやるという２段構えのパワープレイを実施。（やりおる）。これが意外とワークしているらしい。

 * お客様向け(売れ行きのよいタグ抽出)  
 メルカリであまり売れない商品への人気タグの推薦にLLMを利用。ログから売上がよい商品リストをとってきて、そのよい商品ページの情報から、LLNに売上をよくするエンティティを抽出してと依頼して生成している。その後、抽出したタグやテキストをメルカリの出品画面にレコメンドする。例えば、アニメや漫画の缶バッチなどであれば｀バラ売り可｀みたいなのがよいタグだったりするそういうタグを抽出するのに利用しているようだが、LLMなので嘘を言ったりする可能性があり、それは**景品表示法違反**する可能性あるが、基本的にハルシネーションの抑止としてまず、RAGのようにincontet larningを利用することで、まずは、ハルシネーションの発生をまずはある程度抑えられる、あとは、UI的な工夫で基本的には自動で付与するのではなく、ユーザさんに確認してもらって付与の判断をしてもらう。そういうUIを工夫することで最終的なリスクはお客さんにとってもらうようにしている。

## 人の力を活用したサービスロボットの研究開発 (Robotics)
* 安藤 健　さん
* パナソニック ホールディングス株式会社

講演者はパナソニックのロボット開発室の室長。
パナソニックのロボット開発の紹介。まーこれと言って無しだったが、以下がパナソニックの自動ロボット（主に宅配）

<img src="https://asset.watch.impress.co.jp/img/ipw/docs/1404/862/4_1_s.jpg" width=300px>

なのだが、最近、電動キックボードがノーヘルで運転できるという特定小型原動機付自転車(以下 特定小型原付)が2023.7に改定されたタイミンと同じタイミングで上記のようなロボットも公道を走り回ってもいいことになったようで、それが驚き！すでに藤沢市をモデルケースに配達の試験などをやっているらしい。基本ロボットは半自動（リモート監視）で動作していりょうです。１人のオペレーターが今は最大４台を監視しているが、これでは人件費的にペイしない（ロボットも高いので）ので人件費がペイするのは１人で２０台を監視できないとダメみたい。


##  実世界AIサービスのための”ポジティブな”人物行動理解 (Computer Vision)
* 米谷 竜　さん
* 株式会社サイバーエージェント

今年の４月にサイバーエージェントAiLabで、人物行動理解というプロジェクトを立ち上げた人。このプロジェクトに参加している研究員は３名。
サイバーエージェントは基本的には広告屋さんなので、店内のサイネージなどの効果的な提示方法などについて基礎的な研究を実施しているみたい。
イメージとしては、店頭にポップ（みかん安売り）というのがあった場合に、どれぐらいの人がそのポップをみて、みかんの販売コーナまでいって買ってくれるというのを検証したい。
しかし、店内にカメラをつけまくったりするのはプライバシーの問題として難しいし、そもそも誰が誰かわからんというのがある一方、ビーコンみたいなのがあるけど、、これも専用ハードみたいなのがいる。そこでみんなが持っている携帯に注目して、店のどこをあるいたのかという店内の行動理解というのをやりたいとのこと。

そこで、人物行動理解というのは基本的に、携帯電話に入っている慣性センサーを用いて店内のどこを歩いて行ったのかという軌跡を再現するという研究。
SLAMを携帯電話の慣性センサーを用いてやるみたいなイメージ。今回の研究では、購買履歴、店内情報を考慮（購買情報にみかんがあれば必ずみかんの販売しているポイントへ行っている）というのを利用して最初に推定したパスを特定のポイント（みかん販売のところ）を必ず通るようにネットワークを最適化して精度を上げている。

## デジタルゲームのための自然言語処理　①倫理性の階層的考慮 (NLP)
* 森 友亮　さん
* 株式会社スクウェア･エニックス

**あとで個人的に質問をしにいってお話を伺ったで下記にはその情報につても公演情報にプラスされています。**

登壇者はスクウェア･エニックスのAIリサーチャーの方。公演は２つにわかれており、１つ目はLLMが生成する内容についてどう倫理性をもたせればいいのかという話。
想定タスクはNPCがセリフを生成したらどういうことに気をつけないといけないのか？ということに関する問題提起。

一言でいうと、「ゲームの中の悪役が倫理的に反するセリフを言ってほしいがそれを実現するにはどうすればいいのか？」という感じの話。

ゲームの中の世界と現実の正解では倫理観が違うし、既存のLLMはあたりまえだけど、現実の世界の倫理観を逸脱しないように調整されている。

## デジタルゲームのための自然言語処理　②小さなモデルの活用 (NLP)
* 森 友亮　さん
* 株式会社スクウェア･エニックス

続きで、ゲームの中でNLP的なタスクを動作させるにはどうするのか？という話。
基本的には今は２つの選択子がある。

* サーバーサイドで実施する。
* **アプリ（ゲーム機本体）で実施する。**

今回はゲーム機側で動作させるにはどうするのかというのを紹介。
個人的に質問に言ったのだが、本日現在において、いわゆるコンシューマー機（スイッチ、PS5, PC etc)においてゲームとしていわゆるNLP的な動作をするゲーム（本来の意味でゲームとしてワークしているもの）は販売されていないという話であった。生成AIで０ベースで喋らせているサービス、みんなが使えるというのであれば、[AI lain](https://ai.anique.jp/)ぐらいであろうとのこと。でもlainってwebじゃんといったらそうだった！とのこと。なので生成AIでセリフを社べているのはまだないということになる。他の人でスクウェア･エニックスって、[ポートピア連続殺人事件 犯人はヤス！](https://www.jp.square-enix.com/ai-tech-preview/portopia/jp/)をAI化してましたよね？と言われていが、あれば条件分岐などゲームドリブンを自然言語できるがセリフの生成はやってない（リクスが大きい）とのこと。あとあれゲームじゃねーし。技術デモだしとのこと。

それはいいとして、端末側でNLPを動かすためにはGPUを使うのではなく、CPUでやる方向とのこと、ゲーム機のGPUは本来の意味で、ゲーム画面の描画のために使うので、CPU推論となる。今のゲーム機であれば、GPT-2(mediam 0.3B)程度なら比較的CPUでも動作するので実装可能とのこと。動作方式としては以下の通り。

1. pythorch model →  ONNX形式に変換
2. ONNXはONNX runtimeで`c#`などからで動作可能。ただし、tokenizerが問題になる場合は、tokenizerはc#のpython.NETで独自に書いてやればよい。
3. CTraslate2ならc++から動作するし比較的ラク。

基本的にONNX形式はtokenizerのモデルが別なのでtokenzierをケアしないといけないが、`GGUF`というモデル形式はトークナイザーが内包されているのでより便利になるみたい。あと、huggingface とUnreal Engineが提携してやりはじめているので、ゲームでNLPを実装するのがより楽になると思われるとのこいと。

サーバー vs アプリの場合について以下のような利点・欠点あり

* サーバを使う場合  
大規模言語モデルなどの大きいモデルを扱うにはどうしてもサーバーサイドではないとダメ,しかしながらゲーム機で利用する場合は以下の点が懸念
  * オンライン限定
  * サーバーが停止すると遊べない
  * ゲームのパッケージの他に自然言語のサーバーサイドの費用が必要
  * 第三者のサービス（LLM)を利用する場合
    * 性能をゲーム開発者が制御できない。ある日突然、賢くなるなったりして、ゲーム体験に懸念。
    * API利用費、ユーザさんが遊べば遊ぶほど、ゲーム会社がかぶることになる。こりゃたまらん。

* アプリを使う場合  
ゲームタイトル中に言語モデルを含める。
  * 実装面で課題  
    * スペック不足（ハイスペックPCが必要)
    * モデルのアップーデートがしずらい、時関経過ともに新語がでてくるのに対応できない。
  * 実装上の工夫
    * ONNX, ONNX runtimeの利用
    * 軽量化（枝刈り、量子化、蒸留)
    * トークナイザの実行環境依存性の合わせ

上記のようにゲーム体験をそこなわず、遊べるようにするためにはさ、GPUを利用せずにCPUで推論する。一方で、応答速度を速くする必要があるが、stream対応はできない。
全文生成して初めてNGとなるテキストもあるので、streamで逐次だしてしまうとまずい。

あとで口頭できいたら、可能であれば、今はサーバーサイドでやれるのであればそっちほうがお手軽ではあるとのこと。なかなかどっちが悩む。

## グローバル生成AIスタートアップ Stability AIの研究開発アプローチ　(NLP)
* Jerry Chi　さん
* Stability AI Head of Japan

とりあえず、Stability AIは日本市場に注目していて、リクルーティングもしてますよーとのこと。日本では基礎研究はやらずに、応用研究をベースに展開中とのこと。
社員全員PHDを持っているかと思うがそうでもない。手が動く人を募集中とのこと。きになったポイント。

* Stability AIの画像生成AIはめちゃくちゃきれいな画像を生成することにそこまでフォーカスしていない。
　→ midjourneyを意識していると思われる。midjourneyはちょとやばいよね。個人的にnijijourneyもすこ。

## フェルミオン形式による量子近似最適化を用いた電力需要ポートフォリオへの応用
* 笹田 啓太　さん
* TIS株式会社

量子コンピュータを利用用途をさぐるような研究やビジネスのソースを探しておられるような感じ。
普通は量子コンピュータはイジングモデルをもした定式化を実施するだけど、フェルミオン形式のあたらしい定式化を導入。
自由電子のホッピング項のみを考慮したようなモデル。たぶんヒュッケル・モデルというやつなのかな。

この定式化で電力予測の問題を量子コンピュータ（AWS）を利用して解いたとのこと。
量子コンピュータはもう少しQ-bit数が上がってこないと難しいという話もでていた。

## ZOZOTOWN検索における研究開発の取り組みについて
* 山﨑 朋哉　さん
* 株式会社ZOZO

ZOZOの検索の開発の流れなどを説明。各施策につて

* 定量評価
* A/B テスト

などでどのような施策をしてどのようにサービス提供をしていたのかを紹介。

## 機械学習のためのデータ作成UIに関する研究 (HCI)
* 樋口 啓太　さん
* 株式会社Preferred Networks

3Dアノテーションデータ作成のための新しいアノテーション方法の提案。
HCIは、Human Computer Interactionという言葉は初めて聞いた。
