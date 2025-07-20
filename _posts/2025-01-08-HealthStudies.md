---
title: "Quantitative Health Studies on Quality of Life and Social Determinants of Diseases"
date: 2025-01-08
layout: post
category: research
tags: [Statistics, R, Publication, Methodology]
image: "/images/mapping_sf6dv2.png"
---

This page is for the research supervised by and co-authored with [Ye Zhang](https://www.researchgate.net/profile/Ye-Zhang-58), when I worked as a research assistant in the field of health econometrics:

<div class="research-item">
  <p><strong>1. Mapping KDQoL-36 onto EQ-5D-5L and SF-6Dv2 in patients undergoing dialysis in China</strong>: Accepted by <em>Value in Health - Regional Issues</em>.</p>
  <div style="display: flex; gap: 0.5rem;">
    <a href="#" class="custom-button" onclick="toggleAbstract('abstract1'); return false;">Abstract</a>
    <a href="https://github.com/MoonEater0912/ALDVMM_Cross_Validation" target="_blank" class="custom-button">GitHub</a>
  </div>
  <div id="abstract1" style="display:none; border:1px dashed #aaa; padding:0.5rem; margin-top:0.5rem;">
    To develop the mapping algorithms from Kidney Disease Quality of Life-36 (KDQoL-36) scores onto the EQ-5D-5L and SF-6Dv2 utility values among the dialysis patients in China. We used data from a cross-sectional multicenter survey study in China to map KDQoL-36 onto EQ-5D-5L and SF-6Dv2. The conceptual overlap between the KDQoL-36 and the EQ-5D-5L or SF-6Dv2 was evaluated by Spearman’s correlation coefficients. Direct mapping, including OLS, GLM, Beta Regression Model (BRM), Tobit Regression Model (TRM), Censored Least Absolute Deviations model (CLAD) and Adjusted Limited Dependent Variable Mixture Model (ALDVMM), and response mapping, Seemingly UnRelated Ordered Probit Model (SUROPM), were used to derive mapping functions using the dataset. The model performance was assessed by mean absolute error (MAE) and root mean square error (RMSE) using cross-validation. A total of 378 patients (50.53% female; mean [SD] age: 49.05 [13.34]) were included in this study. The mean utility values of EQ-5D-5L and SF-6Dv2 were 0.72 and 0.57, respectively. When mapping to EQ-5D-5L, the ALDVMM with 1 component was the best-performing model (MAE = 0.1579, RMSE = 0.2289). When mapping to SF-6Dv2, the TRM was the best-performing model (MAE = 0.1108, RMSE = 0.1508). Generally, KDQoL-36 subscale scores with their square was the optimal predictor set among each model. Overall, models using KDQoL-36 subscale scores showed better fit than using the Kidney Disease Component Summary. ALDVMM and TRM models with the KDQoL-36 scores can be used to predict the EQ-5D-5L and SF-6Dv2 utility values, respectively, among dialysis patients in China.
  </div>
</div>

<div class="research-item">
  <p><strong>2. Socio-demographic characteristics associated with SF-6D v2 utility scores in patients undergoing dialysis in China: Contributions of the Quantile Regression</strong>: Accepted by <em>Health and Quality of Life Outcomes</em>.</p>
  <div style="display: flex; gap: 0.5rem;">
    <a href="#" class="custom-button" onclick="toggleAbstract('abstract1'); return false;">Abstract</a>
    <!-- <a href="https://github.com/MoonEater0912/ALDVMM_Cross_Validation" target="_blank" class="custom-button">GitHub</a> -->
  </div>
  <div id="abstract2" style="display:none; border:1px dashed #aaa; padding:0.5rem; margin-top:0.5rem;">
    Generic preference-based instruments, such as the Short Form 6-Dimensions (SF-6D) and EuroQol 5-Dimensions (EQ-5D), can generate utility scores that facilitate the estimation of health-related quality of life (HRQoL) which is commonly used in cost-utility analysis. This study investigated the associations between utility scores and potential socio-demographic factors in Chinese patients with dialysis using quantile regression. Patients were recruited in a multicenter survey conducted between November 2023 and January 2024 for dialysis patients in China. Patient responses to the SF-6D version 2 (SF-6D v2) instruments were used to calculate utility scores. The relationships between utility scores and potential socio-demographic factors were examined using both Ordinary Least Squares (OLS) and quantile regression models. The Wald test was employed to test the differences in coefficients across quantiles in quantile regression. Model performance was assessed using 5-fold cross-validation. A total of 378 patients were included. Age, education level, having a loan due to illness, currently working, monthly income > 8000 and number of comorbidities were associated with utility scores. The quantile regression coefficients and Wald test suggested that the size of the associations between the utility scores and factors varied along with the utility score distribution. Quantile regression yielded more accurate fitted and predicted values compared to OLS regression. Quantile regression offers a valuable complement in analyzing factors associated with utility scores among Chinese dialysis patients. For policymakers, differentiated nonclinical strategies may be needed to improve HRQoL across varying health states within this population.
  </div>
</div>

<script>
function toggleAbstract(id) {
  var elem = document.getElementById(id);
  if (elem.style.display === "none") {
    elem.style.display = "block";
  } else {
    elem.style.display = "none";
  }
}
</script>