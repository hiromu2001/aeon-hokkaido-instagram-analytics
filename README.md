# aeon-hokkaido-instagram-analytics

イオン北海道公式Instagramの投稿を対象に、**統計分析・自然言語処理（NLP）・画像解析・機械学習を用いて、エンゲージメント要因を分析する研究プロジェクト**です。

> **Disclaimer**  
> 本リポジトリは個人研究用であり、イオン北海道株式会社の公式プロジェクトではありません。公開情報または適切な権限のもとで取得したデータのみを利用し、Meta/Instagramの利用規約・APIポリシー・社内規程を遵守します。

## 研究の狙い

InstagramはXよりも視覚情報の比重が大きいため、キャプションだけでなく、**画像・動画・カルーセル・画像内テキスト・色・構図・商品/人物の写り方**まで含めたマルチモーダル分析を行います。

主な研究質問は次の通りです。

- 投稿テーマ（商品、販促、地域、季節、CSR等）は likes / comments とどう関連するか
- 画像・動画・カルーセルなどの投稿形式は反応とどう関連するか
- 色、明るさ、コントラスト、構図、画像内文字量、人物・商品・食品の有無などの視覚特徴は反応とどう関連するか
- キャプションの情報性・感情性・販促性・CTA・価格表記・地域性は反応とどう関連するか
- 「北海道」「道産」「地域名」「店舗名」などの地域性は反応と関連するか
- テキスト・画像・投稿条件を組み合わせると、将来のエンゲージメントをどの程度予測できるか

## 研究設計の基本方針

Instagramの likes / comments は典型的なカウントデータで、分散が平均を大きく上回ることが多いため、主たる統計モデルは **Poisson回帰ではなく、過分散を確認した上でNegative Binomial回帰を第一候補**とします。ゼロが過剰な場合に限りzero-inflated / hurdle modelも検討します。

機械学習では、テキスト・画像・メタデータを別々に評価したうえで統合し、**time-based holdout**で将来投稿への汎化性能を確認します。SHAP等は予測モデルの説明に用いますが、因果効果とは解釈しません。

## 分析パイプライン

```text
Instagram posts
   ├─ Caption
   │    ├─ topic / category
   │    ├─ sentiment / emotion
   │    ├─ CTA / price / hashtag / emoji
   │    └─ text embedding
   │
   ├─ Image / Carousel / Reel
   │    ├─ CLIP/SigLIP-style embedding
   │    ├─ OCR
   │    ├─ product / food / person / face
   │    ├─ color / brightness / contrast / symmetry
   │    └─ composition / text-area / visual complexity
   │
   └─ Metadata
        ├─ posting time / weekday / season
        ├─ media type
        └─ public or authorized Insight metrics
             ↓
      EDA + Count Regression
             ↓
      ML prediction + ablation
             ↓
      SHAP / robustness checks
```

## 先行研究

本研究は、Instagramのブランド投稿について、視覚・文章・投稿条件とエンゲージメントの関係を分析した先行研究をベースにしています。特に重要な研究は以下です。

- Rietveld et al. (2020): 59ブランド・約46,900投稿。視覚/文章の感情・情報訴求を機械学習で抽出し、Negative Binomial回帰でlikes/commentsを分析。  
  https://doi.org/10.1016/j.intmar.2019.06.003
- Philp, Jacobson & Pancer (2022): 食品マーケティングのInstagram画像をComputer Visionで分析し、食品の視覚的特徴とengagementの関係を検討。  
  https://doi.org/10.1016/j.jbusres.2022.05.078
- Sharma & Peng (2024): 90のfood influencer accountから53,894画像を分析し、視覚美学・食品特性とlikes/commentsの関係を検討。  
  https://doi.org/10.1080/10410236.2023.2175635
- Argyris et al. (2020): 45,000枚超のInstagram画像をDeep Learningで分類し、visual congruenceとbrand engagementを分析。  
  https://doi.org/10.1016/j.chb.2020.106443
- OTA Instagram study: 6,083投稿・109個のtext/visual/social featuresを用い、XGBoostによる重要特徴選択＋Negative Binomial回帰。  
  https://doi.org/10.1080/13683500.2023.2278087
- Food brand study (2026): 食品ブランドInstagram投稿を機械学習＋visual framingで類型化し、Negative Binomial回帰でengagementを分析。  
  https://doi.org/10.1108/JPBM-11-2024-5602

詳細は [`docs/literature_review.md`](docs/literature_review.md) と [`docs/references.md`](docs/references.md) を参照してください。

## 予定ディレクトリ

```text
.
├── README.md
├── docs/
│   ├── literature_review.md
│   ├── research_plan.md
│   └── references.md
├── src/              # 取得・前処理・特徴抽出
├── notebooks/        # EDA / modeling
├── data/
│   ├── raw/          # Git管理外
│   ├── interim/      # Git管理外
│   └── processed/    # 公開可能な派生データのみ
└── reports/
```

## ステータス

**Planning / Literature Review**

まず500投稿程度でpilot analysisを行い、データ分布・取得可能指標・特徴量設計を確認してから本分析へ拡張します。
