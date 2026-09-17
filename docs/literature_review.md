# 先行研究レビュー — Instagram Engagement Analytics

## 1. レビューの目的

本レビューは、イオン北海道公式Instagramを対象にした研究設計について、次の問いに根拠を与えるために作成する。

1. 何を特徴量として取るべきか
2. likes / commentsをどう統計モデル化すべきか
3. 画像とキャプションをどう統合すべきか
4. 食品・小売という業種固有の要因をどう扱うべきか
5. 機械学習による予測と統計的説明をどう分離すべきか

---

## 2. ブランド投稿研究の基礎

### de Vries, Gensler & Leeflang (2012)

ブランド投稿のvividness、interactivity、content typeなどとlikes/commentsの関係を分析した初期の代表的研究。Instagram専用ではないが、その後のブランドSNS研究で広く使われる設計の基礎となる。

- vividness：画像・動画等のリッチさ
- interactivity：質問・リンク・呼びかけ等
- outcomeをlikesとcommentsに分ける

DOI: https://doi.org/10.1016/j.intmar.2012.01.003

**本研究への示唆**：Instagramでも「投稿形式」「CTA」「質問」「内容タイプ」を基本特徴として残す。

---

## 3. Instagramの視覚・テキストを同時に扱う研究

### Rietveld et al. (2020)

Instagram上の59ブランド、約46,900投稿を対象に、視覚・文章からemotional / informative appealを機械学習で抽出し、likes/commentsをNegative Binomial回帰で分析した。

DOI: https://doi.org/10.1016/j.intmar.2019.06.003

重要な点：

- likesとcommentsを別々に分析
- 投稿時刻、曜日、年、hashtag数、followers等をcontrol
- count outcomeの過分散を検定
- PoissonよりNegative Binomialが適合
- visual brand centrality / product centralityを扱う
- text中のbrand mention、product mention、deal、price等を区別

**本研究への示唆**：

イオン北海道Instagramでも、単純なsentimentではなく、次を明示的に抽出する。

- brand centrality
- product centrality
- price / discount mention
- information vs emotion
- posting time / weekday / hashtag count

---

## 4. 食品画像・Computer Vision

### Philp, Jacobson & Pancer (2022)

食品マーケティングのInstagram投稿を対象に、Google Vision AIを使って食品画像の視覚特徴を抽出し、engagementとの関係を分析した。

DOI: https://doi.org/10.1016/j.jbusres.2022.05.078

研究では、画像がどの程度「典型的な食品」として認識されるかがengagementと関連することを示している。

**本研究への示唆**：

イオン北海道では食品投稿が多いことが想定されるため、単なる画像有無ではなく、

- food / non-food
- 商品単体 / 調理済み / 食卓・利用シーン
- 商品の典型性
- 商品が画像中央にあるか
- 背景の複雑さ

などを視覚特徴として検討する価値がある。

### Sharma & Peng (2024)

90のfood influencer accountから53,894画像を収集し、visual aestheticsとcalorie densityがlikes/commentsにどう関係するかをComputer Visionで分析。

DOI: https://doi.org/10.1080/10410236.2023.2175635

報告された視覚特徴には、色、brightness、colorfulness、complexity、repetition等が含まれる。

**本研究への示唆**：

画像から次を定量化する。

- brightness
- saturation / colorfulness
- warm-color ratio
- contrast
- entropy / visual complexity
- repetition / symmetry

---

## 5. Deep Learningによる画像テーマ分析

### Argyris et al. (2020)

45,000枚超のInstagram画像をDeep Learningで分類し、visual congruenceとbrand engagementの関係を検討。

DOI: https://doi.org/10.1016/j.chb.2020.106443

**本研究への示唆**：

固定ラベルだけでなく、CLIP / SigLIP等のvisual embeddingを使って、画像の意味空間を数値化する。

具体的には、

- 商品画像
- 人物画像
- 売場
- 料理
- イベント
- 風景 / 地域
- チラシ的デザイン

といった視覚テーマをクラスタリングできる可能性がある。

---

## 6. マルチモーダル予測

### Predicting user engagement with textual, visual, and social media features for online travel agencies' Instagram posts

6,083投稿について109個のtextual / visual / social featuresを抽出し、XGBoostで重要特徴を選び、Negative Binomial回帰でlikesとの関連を推定。

DOI: https://doi.org/10.1080/13683500.2023.2278087

**本研究への示唆**：

説明モデルと予測モデルを一つに混ぜず、

1. 理論ベースのcount regression
2. XGBoost / LightGBM / CatBoostによる予測
3. SHAPによる予測上の重要度

の3層に分ける。

また、text-only / image-only / metadata-only / multimodalのablation comparisonを行う。

---

## 7. 食品ブランドに特化した最新研究

### Nudging consumer engagement for food brands (2026)

食品ブランドのInstagram投稿をmachine learningとvisual framingで類型化し、post typology / modalityとengagementの関係をNegative Binomial回帰で分析。

DOI: https://doi.org/10.1108/JPBM-11-2024-5602

研究ではsocioemotional orientation、infotainment、transformational等の投稿類型が検討されている。

**本研究への示唆**：

イオン北海道向けの内容カテゴリを、単なる「商品」「セール」だけでなく次のように整理する。

- informational
- promotional
- infotainment
- socioemotional
- transformational / lifestyle
- seasonal
- local / regional
- corporate / CSR

---

## 8. 視覚美学・構図

### Perfect social media image posts: symmetry and contrast influence consumer response (2021)

実験と610件のInstagram field dataを用いて、symmetryとcontrastがlikes/comments等にどう関係するかを検証。

DOI: https://doi.org/10.1108/EJM-09-2018-0629

### Visual aesthetics and presentation modality in luxury fashion brand communication (2020)

15ブランド・40,679投稿を対象に、visual aestheticsとvideo/static modalityの関係を検討。

DOI: https://doi.org/10.1108/JFMM-02-2019-0019

### Visual strategies of luxury and fast fashion brands on Instagram (2023)

画像中のbrand name、logo、embedded text等とengagementの関係を分析。

DOI: https://doi.org/10.1016/j.jretconser.2023.103517

**本研究への示唆**：

OCRだけでなく、

- text-area ratio
- logo / brand-name visibility
- image symmetry
- contrast
- color distribution
- static / carousel / reel

を取得候補とする。

---

## 9. 人物・顔

### Bakhshi, Shamma & Gilbert (2014)

Instagram写真における顔の有無とlikes/commentsの関係を大規模データで分析した代表研究。

DOI: https://doi.org/10.1145/2556288.2557403

**本研究への示唆**：

画像に人がいるか、顔があるかは視覚特徴として保持する。ただし、年齢・性別などのセンシティブ属性推定は本研究の目的には不要であり、原則実施しない。

---

## 10. Captionと画像の関係

### Adam (2025/2026), How Do Image Captions Drive Consumer Engagement on Social Media?

402ブランド・95,155のsingle-image postとオンライン実験を用い、captionが単に画像を説明するだけでなく、画像に新しい意味・解釈を追加する「caption extension」がengagementと関係することを検討。

DOI: https://doi.org/10.1177/10949968251352408

**本研究への示唆**：

captionとimageを別々に評価するだけでなく、**caption-image semantic similarity / complementarity**を特徴量にする。

例：

- CLIP image embedding
- caption embedding
- cosine similarity
- caption extension score

画像と文章が同じ内容を繰り返しているか、別の情報を足しているかを分析する。

---

## 11. Platform差・将来のX比較

### When they like and when they comment: drivers of consumer engagement on social media (2026)

85ブランド・100万件超のTwitter / Instagram投稿を用い、platform affordance、brand origin、product type等とengagementの関係をzero-inflated mixed-effects regressionで比較。

DOI: https://doi.org/10.1108/EJM-12-2024-1024

**本研究への示唆**：

Instagram単独研究を完了した後、`aeon-hokkaido-x-analytics`と接続し、

- 同一企業
- 異なるplatform
- 類似キャンペーン / 同時期

でのcross-platform comparisonを行う価値がある。

---

## 12. 方法論として採用する事項

先行研究から、本プロジェクトでは次を原則とする。

### Outcome

- likesとcommentsを分ける
- authorized Insightsが使える場合はsaves / shares / reach / views等も別々に分析
- 一つの「engagement score」だけに集約しない

### Count data

- 過分散診断
- Poisson vs Negative Binomial比較
- excess zerosがある場合のみzero-inflated / hurdle
- 複数アカウントを扱う場合はmixed-effectsも検討

### Controls

- 曜日
- 時間帯
- 月 / 季節
- 長期trend
- follower count（投稿時点の値が取得可能なら）
- campaign / sweepstakes
- media type

### Human coding

理論的に重要なカテゴリは、モデルの自動推定だけに頼らず、人手coded sampleを作る。

- 100〜200投稿程度を二重コーディング
- Cohen's kappaまたはKrippendorff's alpha
- 不一致カテゴリを再定義

### Predictive modeling

- random splitではなくtime-based split
- text-only / image-only / metadata-only / multimodalを比較
- baselineを必ず置く
- SHAPは因果として解釈しない

---

## 13. 本研究の独自性

既存研究の単純な再現ではなく、次を追加する。

1. **北海道という地域性**を定量化する
2. **総合小売業**として食品・衣料・住居余暇・イベント・CSR等を横断する
3. 画像内の価格・販促文言をOCRで取り込む
4. caption-image semantic relationshipを扱う
5. CLIP系embedding＋日本語caption embeddingを統合する
6. 投稿の説明（count regression）と将来予測（ML）を分離する
7. 将来的に同一企業のXデータとcross-platform比較できる設計にする

この組み合わせにより、「どの投稿が伸びたか」ではなく、**どのような内容・表現・視覚構成が反応と関連し、そのパターンが将来投稿にも再現するか**を検証できる。
