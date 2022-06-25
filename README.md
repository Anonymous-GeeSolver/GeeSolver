# GeeSolver

## Overview of GeeSolver

We first design a generic and efficient baseline model (GeeSolver model) to break captchas with a ViT-based latent representation extractor and a captcha decoder. Then, in stage I, we leverage unlabeled captchas to train our latent representation extractor with the MAE-sytle paradigm. In stage II, the same unlabeled captchas and a few labeled captchas (additional) are used to train the captcha decoder with semi-supervised method.

## Insights

- ViT Encoder

Numerous difficult-to-attack captcha schemes that “damage” the standard font of characters are similar to image masks. In this case, the MAE-based paradigm is very suitable for obtaining a latent feature extractor (ViT encoder) with the ability to infer characters from local information. 

- Captcha Decoder

Text-based captchas have the common characteristics that text is arranged horizontally from left to right, which inspired the design of a sophisticated sequence-based decoder to recognize captcha more efficiently. 

The above insights make GeeSolver (composed of a ViT encoder and a captcha decoder) outperforms the state-of-the-arts by a large margin.

## Defense Points

To defend against our attack, we have also designed two security mechanisms, i.e., the **overly skewed text** and the **unpredictable background**.

- **Overly Skewed Text** (making it difficult for captcha decoder) 

Since GeeSolver contains a sequence-based decoder, overly skewed text will affect performance, which is also proved in the *Microsoft* captchas of dataset A. However, the overly skew text is easily corrected by the preprocessing algorithm. Besides, solver can still achieve a high success rate with sufficient unlabeled samples.

- **Unpredictable Background**  (making it difficult for ViT encoder)

Unpredictable background is rarely considered in the existing captcha design. The core of GeeSolver is MAE, which trains the ViT encoder through the reconstruction task of inferring entire characters from their parts. 
After introducing unpredictable backgrounds, MAE will pay much attention to recovering meaningless and complex backgrounds, which has a huge negative impact on the training of the VIT encoder. 
As shown below, we show the reconstructed captchas of MAE using unpredictable backgrounds, more reconstructed cases can be seen in the [reconstructed cases](https://github.com/Anonymous-GeeSolver/GeeSolver/edit/main/DefensePoints). For each triplet, we exhibit the ground truth (top), the masked captcha (middle), and MAE reconstruction (bottom). 
In the case of the same mask, MAE cannot fully recover the captcha characters due to the interference of complex background noise, which indicates that adding unpredictable background can prevent MAE from extracting high-quality representations.
After adding unpredictable backgrounds to Google captchas, the accuracy of GeeSolver drops from 90.7% to 3%. It is worth noting that adding unpredictable backgrounds to existing captchas is simple and will not increase the difficulty of recognition for users.

<div align=center><img src="https://github.com/Anonymous-GeeSolver/GeeSolver/blob/main/DefensePoints/new_captcha_part.png" width="950px">



