# Defense Points


## Overly Skewed Text
The Microsoft scheme in Dataset A design captchas with overly skewed text, as shwon below. Since the captcha decoder is designed according to the common characteristics of captcha images (i.e., the text is arranged horizontally from left to right), overly skewed captchas are inconsistent with our original intention. GeeSolver only obtains an accuracy of 22.67% when using 1000 unlabeled samples.

However, the overly skew text is easily corrected by the preprocessing algorithm. Besides, solver can still achieve a high success rate with sufficient unlabeled samples.
<div align=center> <img src="https://github.com/Anonymous-GeeSolver/GeeSolver/blob/main/DefensePoints/ms.png" width="350px"></div>

## Unpredictable Background

We propose a security feature called unpredictable background to defend against GeeSolver, as shown below.

For each triplet, we exhibit the ground truth (top), the masked captcha (middle), and MAE reconstruction (bottom).

In the case of the same mask, MAE cannot fully recover the captcha characters due to the interference of complex background noise, which indicates that adding unpredictable background can prevent MAE from extracting high-quality representations. After adding unpredictable background to Google captchas, the accuracy of GeeSolver drops from 90.7% to 3%.

<div align=center> <img src="https://github.com/Anonymous-GeeSolver/GeeSolver/blob/main/DefensePoints/new_captcha.png" width="850px"></div>
