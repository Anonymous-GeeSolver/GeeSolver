# GeeSolver

## Overview of GeeSolver

We first design a generic and efficient baseline model (GeeSolver model) to break captchas with a ViT-based latent representation extractor and a captcha decoder. Then, in stage I, we leverage unlabeled captchas to train our latent representation extractor with the MAE-sytle paradigm. In stage II, the same unlabeled captchas and a few labeled captchas (additional) are used to train the captcha decoder with semi-supervised method.

## Insights

- ViT Encoder

Numerous difficult-to-attack captcha schemes that “damage” the standard font of characters are similar to image masks. In this case, the MAE-based paradigm is very suitable for obtaining a latent feature extractor (ViT encoder) with the ability to infer characters from local information. 

- Captcha Decoder

Text-based captchas have the common characteristics that text is arranged horizontally from left to right, which inspired the design of a sequence-based decoder to recognize captcha more efficiently. 

The above insights make GeeSolver (composed of a latent feature extractor and a sophisticated decoder) outperforms the state-of-the-arts by a large margin.

## Defense Points

We propose a security feature called unpredictable background to defend against GeeSolver, as shown below.

For each triplet, we exhibit the ground truth (top), the masked captcha (middle), and MAE reconstruction (bottom).

In the case of the same mask, MAE cannot fully recover the captcha characters due to the interference of complex background noise, which indicates that adding unpredictable background can prevent MAE from extracting high-quality representations. After adding unpredictable background to Google captchas, the accuracy of GeeSolver drops from 90.7% to 3%.

<img src="https://github.com/Anonymous-GeeSolver/GeeSolver/blob/main/DefensePoints/new_captcha.png" width="950px">



