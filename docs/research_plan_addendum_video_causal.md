# Research Plan Addendum — Reels Video Causal Inference

本ファイルは `docs/research_plan.md` の高度拡張。

## Additional Research Question

### RQ8: Dynamic Video Causality
Reels内の視覚特徴（商品、価格、地域訴求、人物、調理シーン等）が**どのタイミングで現れるか**を時変Treatmentとして扱ったとき、視聴者反応への因果効果を推定できるか。

## Positioning

Primary analysisにはしない。

1. 通常のInstagram分析（EDA / count regression / multimodal ML）を完成
2. Reelsの十分なサンプル数とTreatment variationを確認
3. `gpi_pack` Video-as-Treatmentのfeasibilityを検証
4. 条件が成立する場合のみ因果推論へ進む

## Primary reference

Nakamura et al. (2026), *Causal Inference with Video Features as Treatments*, arXiv:2607.06126.  
https://arxiv.org/abs/2607.06126

詳細は [`video_causal_inference.md`](./video_causal_inference.md) を参照。
