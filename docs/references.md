# References

先行研究のうち、本研究設計に直接関係する文献をまとめる。原則として査読論文を優先し、DOIを記載する。

## Core: Brand posts / Engagement

1. de Vries, L., Gensler, S., & Leeflang, P. S. H. (2012). Popularity of Brand Posts on Brand Fan Pages: An Investigation of the Effects of Social Media Marketing. *Journal of Interactive Marketing, 26*(2), 83–91.  
   https://doi.org/10.1016/j.intmar.2012.01.003

2. Rietveld, R., van Dolen, W., Mazloom, M., & Worring, M. (2020). What You Feel, Is What You Like: Influence of Message Appeals on Customer Engagement on Instagram. *Journal of Interactive Marketing, 49*, 20–53.  
   https://doi.org/10.1016/j.intmar.2019.06.003  
   **Relevance:** 約46.9K投稿・59ブランド、visual/text appeal、Negative Binomial、likes/comments別分析。

3. Schultz, C. D. (2017). Proposing to your fans: Which brand post characteristics drive consumer engagement activities on social media brand pages? *Electronic Commerce Research and Applications, 26*, 23–34.  
   https://doi.org/10.1016/j.elerap.2017.09.005

## Food / Retail / Computer Vision

4. Philp, M., Jacobson, J., & Pancer, E. (2022). Predicting social media engagement with computer vision: An examination of food marketing on Instagram. *Journal of Business Research, 149*, 736–747.  
   https://doi.org/10.1016/j.jbusres.2022.05.078  
   **Relevance:** Food marketing + Computer Vision。イオン北海道との業種近接性が高い。

5. Sharma, M., & Peng, Y. (2024). How Visual Aesthetics and Calorie Density Predict Food Image Popularity on Instagram: A Computer Vision Analysis. *Health Communication, 39*(3), 577–591.  
   https://doi.org/10.1080/10410236.2023.2175635  
   **Relevance:** 53,894画像・90 food influencer accounts。色・complexity等のvisual aesthetics。

6. Nudging consumer engagement for food brands: a machine learning and visual framing-based typological approach. (2026). *Journal of Product & Brand Management, 35*(1), 79–98.  
   https://doi.org/10.1108/JPBM-11-2024-5602  
   **Relevance:** food brand Instagram、machine learning + visual framing + Negative Binomial。

## Multimodal / Machine Learning

7. Predicting user engagement with textual, visual, and social media features for online travel agencies' Instagram post: evidence from machine learning. (2024). *Current Issues in Tourism, 27*(22).  
   https://doi.org/10.1080/13683500.2023.2278087  
   **Relevance:** 6,083 posts, 109 features, XGBoost + Negative Binomial。multimodal設計の直接的参考。

8. Argyris, Y. A., Wang, Z., Kim, Y., & Yin, Z. (2020). The effects of visual congruence on increasing consumers’ brand engagement: An empirical investigation of influencer marketing on Instagram using deep-learning algorithms for automatic image classification. *Computers in Human Behavior, 112*, 106443.  
   https://doi.org/10.1016/j.chb.2020.106443  
   **Relevance:** 45,000画像超、deep learning image classification。

9. Decoding influencer marketing effectiveness on Instagram: Insights from image, text, and influencer features. (2025). *Journal of Retailing and Consumer Services, 85*, 104285.  
   https://doi.org/10.1016/j.jretconser.2025.104285  
   **Relevance:** image visual/topic + text topic + account featuresを組み合わせたengagement prediction。

## Visual Aesthetics / Composition

10. Perfect social media image posts: symmetry and contrast influence consumer response. (2021). *European Journal of Marketing, 55*(6), 1747–1779.  
    https://doi.org/10.1108/EJM-09-2018-0629  
    **Relevance:** experiment + 610 Instagram posts。symmetry / contrast。

11. Exploring the role of visual aesthetics and presentation modality in luxury fashion brand communication on Instagram. (2020). *Journal of Fashion Marketing and Management, 24*(1), 15–31.  
    https://doi.org/10.1108/JFMM-02-2019-0019  
    **Relevance:** 40,679 posts, 15 brands。visual aesthetics × video/static modality。

12. Visual strategies of luxury and fast fashion brands on Instagram and their effects on user engagement. (2023). *Journal of Retailing and Consumer Services, 75*, 103517.  
    https://doi.org/10.1016/j.jretconser.2023.103517  
    **Relevance:** logo / brand name / embedded text等の画像内要素。

13. Permell, S. R., & Pacheco, B. G. (2024). Consumer Responses to Elements of Visual Esthetics on a Brand’s Instagram Page. *Journal of Promotion Management, 30*(4), 583–614.  
    https://doi.org/10.1080/10496491.2023.2289931  
    **Relevance:** visual complexityとcolor combinationの実験的検証。

## Faces / People

14. Bakhshi, S., Shamma, D. A., & Gilbert, E. (2014). Faces engage us: photos with faces attract more likes and comments on Instagram. *Proceedings of CHI 2014*, 965–974.  
    https://doi.org/10.1145/2556288.2557403  
    **Relevance:** face presenceとengagement。人物属性推定を行わずpresenceのみを見る設計の参考。

## Caption / Image–Text Relationship

15. Adam, Z. (2025/2026). How Do Image Captions Drive Consumer Engagement on Social Media? *Journal of Interactive Marketing, 61*(3).  
    https://doi.org/10.1177/10949968251352408  
    **Relevance:** 95,155 single-image posts・402 brands + experiment。caption extensionというimage-text complementarityに近い概念。

## Cross-platform

16. When they like and when they comment: drivers of consumer engagement on social media. (2026). *European Journal of Marketing, 60*(6), 1395–1430.  
    https://doi.org/10.1108/EJM-12-2024-1024  
    **Relevance:** 85 brands・100万件超のTwitter/Instagram posts。platform affordance比較、zero-inflated mixed-effects regression。

## Additional methodological references

17. O'Hara, R. B., & Kotze, D. J. (2010). Do not log-transform count data. *Methods in Ecology and Evolution, 1*(2), 118–122.  
    https://doi.org/10.1111/j.2041-210X.2010.00021.x  
    **Relevance:** count outcomeを安易にlog変換してOLSに入れるより、count modelを使う根拠。

18. Lundberg, S. M., & Lee, S.-I. (2017). A Unified Approach to Interpreting Model Predictions. *NeurIPS 2017*.  
    https://arxiv.org/abs/1705.07874  
    **Relevance:** SHAP。

## Notes

- 各研究の効果方向をイオン北海道へそのまま一般化しない。
- 業界・時期・アルゴリズム・フォロワー構成・Instagram UIの違いによって効果は変わり得る。
- 先行研究は「どの変数を測るべきか」「どのモデルが妥当か」の根拠として利用し、イオン北海道の係数は独自に推定する。
- Meta/Instagram API仕様は学術論文ではなく、実装開始時点の公式developer documentationを別途確認する。
