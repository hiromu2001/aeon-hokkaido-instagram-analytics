# 研究計画 — イオン北海道公式Instagram分析

## 1. 研究目的

イオン北海道公式Instagramの投稿について、投稿内容・キャプション・画像/動画・投稿条件とユーザー反応の関係を、統計分析・NLP・Computer Vision・機械学習で検証する。

観察研究であるため、基本的な結論は「関連」または「予測寄与」とし、因果効果とは区別する。

---

## 2. Research Questions

### RQ1: Content
商品、販促、季節、地域、イベント、CSR、娯楽等の投稿タイプはlikes/commentsとどう関連するか。

### RQ2: Caption
文字数、価格表記、discount表現、CTA、質問、絵文字、hashtag、感情、情報性、地域表現等は反応とどう関連するか。

### RQ3: Visual
明るさ、色、contrast、symmetry、visual complexity、人物/顔、商品、食品、画像内文字量などは反応とどう関連するか。

### RQ4: Modality
single image / carousel / reel / video等のmedia typeで反応は異なるか。

### RQ5: Locality
北海道・道産・地域名・店舗名・地域イベントなど、地域性の強さは反応と関連するか。

### RQ6: Caption × Image
画像とcaptionが意味的に似ている／補完している度合いは反応と関連するか。

### RQ7: Prediction
投稿前に利用可能な特徴だけを使ったとき、将来のlikes/comments等をどの程度予測できるか。

---

## 3. 対象データ

### Pilot
まず500投稿程度。

目的：
- 取得可能なfieldの確認
- likes/commentsの分布確認
- media typeの構成比
- caption / image処理の動作確認
- API/データ取得コストと実装工数の見積り

### Main study
取得可能な期間全体へ拡張。

外部公開情報だけを利用する場合と、アカウント管理権限のあるInstagram Insightsを利用できる場合を分ける。

#### 公開情報ベース
取得可能な範囲で：
- post identifier
- timestamp
- caption
- media type
- visible likes
- visible comments
- media URLまたは解析可能な画像/動画

#### Authorized Insightsが使える場合
取得時点でMetaが提供するmetricsを確認し、利用可能なものを追加する。

候補：
- reach / views
- likes
- comments
- saves
- shares
- profile actions等

※API仕様・metric名・保持期間は変更されるため、実装開始時に公式仕様を再確認する。

---

## 4. 除外・分類ルール

Primary analysisでは原則として、公式アカウント自身が発信した通常feed/reel投稿を対象とする。

別扱い候補：
- giveaway / sweepstakes
- 大型キャンペーン
- repost / collaboration
- duplicate / cross-post
- 災害・緊急告知
- 採用等の特殊用途

キャンペーン投稿は通常投稿より桁違いのengagementになる可能性があるため、

1. 全投稿
2. campaign除外
3. campaign indicator調整

のrobustness checkを行う。

---

## 5. 特徴量

### 5.1 Caption / Text

機械抽出：
- char_count
- token_count
- hashtag_count
- mention_count
- emoji_count
- question / exclamation
- URL
- price mention
- discount mention
- percentage mention
- store name
- region name
- product category keyword

NLP：
- sentence embedding
- topic
- sentiment
- emotion
- promotional / informational / entertaining
- CTA
- local_score
- caption extension / image-text complementarity

日本語モデルは実装時点で比較し、特定モデルを事前固定しない。

### 5.2 Visual

低レベル特徴：
- brightness
- saturation
- colorfulness
- warm color ratio
- contrast
- entropy
- sharpness
- symmetry
- aspect ratio

意味特徴：
- visual embedding (CLIP / SigLIP系)
- food
- product
- person / face presence
- store / shelf
- landscape / local scenery
- event
- text-heavy creative

OCR：
- image_text_count
- text_area_ratio
- price_text
- discount_text
- product name
- date / campaign period

### 5.3 Metadata

- media_type
- carousel_count
- weekday
- hour
- month
- season
- holiday / seasonal-event proximity
- long-term time trend

---

## 6. Human Coding

自動分類だけで重要カテゴリを決めない。

### Pilot coding
100〜200投稿を対象に二名で独立分類する。

候補codebook：
- informational
- promotional
- infotainment
- socioemotional
- lifestyle / transformational
- seasonal
- local / regional
- corporate / CSR
- product-focused
- people-focused
- price-focused

一致度：
- binary / nominal: Cohen's kappa
- multi-rater / missingを含む場合: Krippendorff's alphaも検討

一致度が低いカテゴリは定義を修正して再評価する。

---

## 7. EDA

最初に以下を確認する。

- 投稿数の時間推移
- media type構成
- likes/commentsの平均・中央値・分散・最大値
- zero比率
- mean vs variance
- campaignの外れ値
- weekday/hour別分布
- content category別分布
- visual feature分布
- caption length / hashtagsとの単純関連

平均値だけでなくmedian / quantile / ECDFも使う。

---

## 8. 統計モデル

### Primary outcomes
- likes
- comments

Authorized Insightsが使える場合は、saves / shares等を追加。

### Model selection

1. Poisson
2. overdispersion check
3. Negative Binomial
4. excess zerosが実際に問題になる場合のみzero-inflated / hurdle

基本モデル例：

```text
log(E[likes_i])
 = β0
 + β1 content_type_i
 + β2 media_type_i
 + β3 local_score_i
 + β4 price_i
 + β5 CTA_i
 + β6 visual_features_i
 + β7 caption_features_i
 + calendar controls
 + trend
```

結果は可能ならIRR = exp(β)で報告する。

### Exposureが取れる場合

reach等の適切なexposure metricが取得できる場合、単純なratioだけでなく、count modelで `log(exposure)` をoffsetとして扱えるか検討する。

---

## 9. 機械学習

目的は因果推定ではなくout-of-sample prediction。

### Baselines
- global median / mean
- Negative Binomial GLM
- Elastic Net on log1p target

### Models
- LightGBM
- CatBoost
- gradient boosting + text embeddings
- multimodal model

### Ablation

必ず比較する。

1. metadata only
2. text only
3. image only
4. metadata + text
5. metadata + image
6. full multimodal

これにより「画像を追加する価値」「captionを追加する価値」が定量化できる。

### Validation

random splitを基本にしない。

- train: 古い70%
- validation: 次の15%
- test: 最新15%

またはrolling / expanding window validation。

### Metrics
- MAE
- RMSE / RMSLE
- Poisson deviance
- Spearman rank correlation

投稿の絶対数予測が難しい場合は、top-decile engagement classificationも補助タスクとして検討する。

---

## 10. Explainability

- SHAP
- permutation importance
- partial dependence / ALE（必要に応じて）

ただし、SHAP値は「モデルが予測に使った情報」であり、投稿施策の因果効果ではない。

---

## 11. Robustness checks

- campaign除外
- giveaway除外
- extreme outlier winsorizationの有無
- likes/comments別モデル
- media type別subsample
- food vs non-food
- pre/post期間
- topic definition変更
- raw count vs exposure-adjusted model

多くの特徴を探索する場合、p-valueの多重比較に注意し、confirmatory analysisとexploratory analysisを分ける。

---

## 12. 因果推論の限界

観察データだけでは、たとえば「動画だからlikesが増えた」とは断定できない。

交絡例：
- 大型キャンペーンほど動画を使う
- 季節イベントほど制作予算が高い
- 人気商品ほど事前に強く販促される
- 投稿時間も担当者が戦略的に決めている

したがって通常分析では「関連」「予測寄与」と表現する。

将来的に社内でA/B testや準実験が可能なら、因果分析を別研究として設計する。

---

## 13. Ethics / Data Governance

- API key / access tokenをGitに入れない
- raw media / raw API responseをpublic repoに置かない
- 一般ユーザーのcomment本文はPrimary analysisでは収集しない
- 個人の属性推定は原則行わない
- 画像中の顔はpresence程度にとどめ、年齢・性別・人種等を推定しない
- Meta/Instagramの利用規約・API条件を実装時に再確認する
- 社内Insightsを使う場合はpublic repoと完全分離する

---

## 14. Roadmap

- [ ] API / データ取得方法を最新仕様で確認
- [ ] 500投稿pilot取得
- [ ] EDA
- [ ] coding scheme作成
- [ ] 100〜200投稿を二重coding
- [ ] OCR / visual features prototype
- [ ] caption embedding prototype
- [ ] Negative Binomial baseline
- [ ] campaign sensitivity analysis
- [ ] image/text ablation
- [ ] LightGBM / CatBoost
- [ ] time-based holdout
- [ ] SHAP
- [ ] main datasetへ拡張
- [ ] report / dashboard
- [ ] X研究とのcross-platform比較を検討
