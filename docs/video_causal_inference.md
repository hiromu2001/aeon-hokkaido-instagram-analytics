# Instagram Reelsの動画因果推論 — Advanced Extension

Status: **Advanced / optional extension**

## 1. なぜ追加するか

通常のInstagram分析では、画像・動画・キャプション・投稿時刻などとlikes/comments等の**関連**を推定する。

一方、Reelsでは「動画の何秒目に、どの視覚要素が出るか」が時間とともに変化する。たとえば、

- 商品が登場する
- 価格・値引きが表示される
- 「北海道産」「道産」等の地域訴求が出る
- 人物が登場する
- 調理シーンが出る
- ロゴが出る
- CTAが表示される

といった特徴は、動画の時間軸に沿って変化する。

このような**時間変化する動画特徴をTreatmentとして扱う因果推論**を、将来的なReels分析の高度拡張として検討する。

---

## 2. 中核となる先行研究

### Nakamura et al. (2026) — Causal Inference with Video Features as Treatments

Kentaro Nakamura, Adam Breuer, Michael H. Crespin, Bryce J. Dietrich, Kosuke Imai (2026).  
**Causal Inference with Video Features as Treatments**. arXiv:2607.06126.

- arXiv: https://arxiv.org/abs/2607.06126
- Research page: https://imai.fas.harvard.edu/research/videocausal/
- Software/docs: https://gpi-pack.github.io/video_as_treatment.html

この研究は、動画を固定長segmentへ分割し、各segmentで存在する視覚特徴を**時変Treatment sequence**として扱う。

標準的な因果推論が難しい理由として、動画には高次元かつ潜在的な交絡特徴が大量に存在し、TreatmentとOutcomeの両方へ動的に関連する点を挙げている。

提案法では、深層生成モデルで動画を再構成し、その内部表現を動画内容の低次元表現として利用して因果推定を行う。

論文では、

1. 10,000個のSuper Mario Bros. levelを使ったground-truth benchmark
2. 2020年米国大統領選のTV広告への実データ応用

で方法を検証している。

本研究にとって重要なのは、**「どの動画特徴が、どのタイミングで現れると、視聴者反応がどう変化するか」**を明示的に問いとして扱える点である。

> 注意：2026年9月時点ではarXiv preprintとして扱い、査読済み手法と同じ確度では扱わない。

---

## 3. gpi_pack

`gpi_pack` 0.2.1ではVideo-as-Treatmentが実装されている。

Docs: https://gpi-pack.github.io/

現行docsでは、

- sequential video treatment
- scalar outcome
- repeated / real-time outcome

をサポートしている。

動画を固定長segmentへ分割し、各segmentについてbinary treatmentを与える。

例：

```text
Reel A
0-2 sec    商品表示       W=1
2-4 sec    商品表示       W=1
4-6 sec    人物のみ       W=0
6-8 sec    価格表示       W=0   # Treatmentを「商品表示」とした場合
```

Treatmentを「価格表示」に変更すれば、同じ動画でも別の因果問いを設定できる。

---

## 4. イオン北海道Instagramで考えられるTreatment

### 商品訴求
- product_visible
- product_closeup
- package_visible
- food_closeup

### 価格・販促
- price_visible
- discount_visible
- percent_off_visible
- campaign_text_visible

### 地域性
- hokkaido_text_visible
- local_product_visible
- region_name_visible
- local_scenery_visible

### 人物・演出
- person_visible
- staff_visible
- cooking_scene
- eating_scene
- hand_interaction

### ブランド
- aeon_logo_visible
- store_exterior_visible
- store_interior_visible

### CTA
- call_to_action_visible
- end_card_visible

Treatmentは最初から大量に作らず、**理論的・実務的に意味のある1〜3個へ絞る**。

---

## 5. 研究質問候補

### RQ-V1
Reelの早い段階で商品を見せる確率を高めた場合、視聴者反応はどう変化するか。

### RQ-V2
価格・値引き情報を動画前半に表示する確率を高めた場合、反応はどう変化するか。

### RQ-V3
「北海道産」「道産」等の地域訴求が動画中に現れる確率を高めた場合、反応はどう変化するか。

### RQ-V4
人物・調理シーン・商品アップのTreatment timingによって、反応の軌跡は異なるか。

---

## 6. Outcome

### 公開データのみの場合
scalar outcomeとして候補：

- likes
- comments
- visible engagement count

ただし、最終的なlikes/commentsは動画視聴以外の要因にも強く影響されるため、因果解釈はかなり慎重に行う。

### Authorized Instagram Insightsが使える場合
より適した候補：

- views / reach
- watch time
- retention-like metrics（取得可能な場合）
- shares
- saves
- profile actions

特にsegment単位または時間軸に沿った視聴反応が取得できる場合、Video-as-Treatmentの設計とより整合する。

> Meta APIで利用可能なmetric名・保持期間・granularityは変更されるため、実装時に公式docsで再確認する。

---

## 7. 重要な限界

### 動画外の交絡

GPIで動画内容の高次元交絡を扱えても、以下は別問題として残る可能性がある。

- 広告出稿量
- 投稿ごとのreach
- キャンペーン規模
- 人気商品の選択
- 季節要因
- 投稿時間
- collaboration
- giveaway
- フォロワー数推移

したがって、可能な限り静的covariatesとして調整し、campaign / giveaway等は感度分析を行う。

### Positivity / overlap

たとえば「価格訴求のあるReelは必ず冒頭に価格を出す」など、Treatment timingがほぼ固定されている場合、因果効果を十分に識別できない可能性がある。

### Outcomeの粗さ

最終likesのみでは、動画内の特定segmentに対する反応と最終engagementを直接結びつけるのは難しい。

### Preprint

Nakamura et al. (2026) は現時点ではpreprint。まずは通常の観察分析・予測分析を完成させ、その後のadvanced extensionとして扱う。

---

## 8. Causal Writability論文との関係

Wang et al. (2026), **A Chosen Future Can Still Be Rewritten: Causal Writability in Video Models**  
arXiv:2609.15980  
https://arxiv.org/abs/2609.15980

これは2026-09-14公開の研究で、動画生成モデル内部の表現へ介入し、物理的に正しい運動を生成結果へ書き戻せるかを調べている。

興味深いが、**Instagram投稿の視覚特徴がengagementへ与える因果効果を推定する手法ではない**。

したがって本プロジェクトでは、

- mechanistic interpretability / video model interventionの関連研究として記録
- 実際のReels因果分析には直接採用しない

という位置づけにする。

---

## 9. 実装ロードマップ

通常のInstagram分析を先に完成させる。

```text
Phase 1
500-post pilot
  ↓
EDA / Negative Binomial
  ↓
Text + Image multimodal ML
  ↓
Reels subsetを抽出
  ↓
Video feature detection prototype
  ↓
Treatment定義
  ↓
segment-level annotation / detection
  ↓
GPI feasibility check
  ↓
Video-as-Treatment causal estimation
```

### 実装前チェック

- [ ] Reels本数が十分か
- [ ] 各Treatmentにvariationがあるか
- [ ] segment分割方法を決める
- [ ] Treatmentを1〜3個に絞る
- [ ] scalar outcomeかrepeated outcomeか決める
- [ ] external covariatesを列挙する
- [ ] positivity / overlap確認
- [ ] gpi_pack最新版のAPI確認
- [ ] NVIDIA Cosmos Tokenizer等の必要GPUコストを見積もる
- [ ] preprintの更新・査読状況を再確認する

---

## 10. 本研究での位置づけ

この手法をPrimary analysisにはしない。

**Primary**
- 内容分析
- Negative Binomial等のcount regression
- multimodal ML
- time-based validation

**Advanced causal extension**
- Reelsのみ
- segment-level video feature treatments
- Generative-AI Powered Inference / Video-as-Treatment

この二段構成にすることで、通常の観察研究から無理に因果を主張せず、データ条件が整った場合のみ高度な因果分析へ進める。
