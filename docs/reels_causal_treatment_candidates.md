# Reels causal treatment candidates

Video-as-Treatmentを試す場合の候補。実装時には1〜3個へ絞る。

| Treatment | 定義例 | 仮説例 | 検出方法候補 |
|---|---|---|---|
| product_visible | segment内に商品が明確に写る | 早期の商品提示と反応が関連する | object/VLM classifier |
| price_visible | 円・¥・価格OCRが存在 | 前半の価格提示が反応へ影響 | OCR + regex |
| discount_visible | %OFF/割引/特価等 | 値引き訴求のtimingが反応へ影響 | OCR + text classifier |
| hokkaido_local_visible | 北海道/道産/地域名/地域景観 | 地域訴求のtimingが反応へ影響 | OCR + VLM/local classifier |
| person_visible | 人物が明確に写る | 人物登場のtimingが反応へ影響 | person detector |
| cooking_scene | 調理動作が見える | 調理シーンが食品投稿の反応へ影響 | video/VLM classifier |
| aeon_logo_visible | AEONロゴが見える | brand cue timingが反応へ影響 | logo detector/OCR |
| cta_visible | 「詳しくは」「チェック」等 | CTAのtimingが反応へ影響 | OCR + classifier |

## 優先候補

初期feasibilityでは次の3つを優先する。

1. `product_visible`
2. `price_visible`
3. `hokkaido_local_visible`

理由：イオン北海道の小売・地域ブランド文脈と直接対応し、OCR/visionで比較的操作的定義を作りやすい。

## 注意

- Treatment definitionは動画を見た後で結果に合わせて変更しない。
- 実装前に少数動画でannotation reliabilityを確認する。
- Treatment prevalenceとtimingのvariationが不足する場合は因果推定を中止する。
