# Implementation gate — Reels causal analysis

ReelsのVideo-as-Treatment因果推論は、以下を満たした場合のみ実装する。

- Reels本数が十分
- Treatment timingにvariationがある
- Treatmentの自動/人手annotation精度が許容範囲
- outcomeが適切
- 外部交絡（campaign / reach / season等）の調整変数が確保できる
- positivity / overlapが成立する
- gpi_pack最新版の前提・APIを確認済み

条件を満たさない場合は、動画特徴は通常の観察分析・予測分析にとどめる。
