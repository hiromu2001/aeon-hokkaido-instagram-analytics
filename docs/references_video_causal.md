# References — Video Causal Inference

## Primary method

1. Nakamura, K., Breuer, A., Crespin, M. H., Dietrich, B. J., & Imai, K. (2026). *Causal Inference with Video Features as Treatments*. arXiv:2607.06126.  
   https://arxiv.org/abs/2607.06126  
   Research page: https://imai.fas.harvard.edu/research/videocausal/  
   **Relevance:** 時間変化する動画特徴をTreatment sequenceとして扱い、生成モデル内部表現を用いて高次元・動的交絡を調整する方法。Reelsの高度拡張に直接関連。2026年9月時点ではpreprint。

## Software

2. GPI: Generative-AI Powered Inference (`gpi_pack`) documentation.  
   https://gpi-pack.github.io/  
   Video-as-Treatment: https://gpi-pack.github.io/video_as_treatment.html  
   **Relevance:** version 0.2.1 docsではVideo-as-Treatmentについてscalar outcome / repeated outcomeをサポート。

## Related, not directly adopted

3. Wang, X., Zheng, H., Yuan, M., Yang, L., & Liu, Z. (2026). *A Chosen Future Can Still Be Rewritten: Causal Writability in Video Models*. arXiv:2609.15980.  
   https://arxiv.org/abs/2609.15980  
   **Relevance:** 動画生成モデル内部へ介入して生成結果を変えるmechanistic interpretability研究。Instagram engagementの因果効果推定手法ではないため、直接の分析手法としては採用しない。
