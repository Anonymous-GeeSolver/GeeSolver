# GeeSolver

## Overview

We first design a generic and efficient baseline model (GeeSolver model) to break captchas with a ViT-based latent representation extractor and a captcha decoder. In stage I, we leverage unlabeled captchas to train our latent representation extractor with the MAE-sytle paradigm. In stage II, the same unlabeled captchas and a few labeled captchas (additional) are used to train the captcha decoder with semi-supervised method.

## Insights

- ViT Encoder

Numerous difficult-to-attack captcha schemes that “damage” the standard font of characters are similar to image masks. In this case, the MAE-based paradigm is very suitable for obtaining a latent feature extractor (ViT encoder) with the ability to infer characters from local information. 

- Captcha Decoder

Text-based captchas have the common characteristics that text is arranged horizontally from left to right, which inspired the design of a sophisticated sequence-based decoder to recognize captcha more efficiently. 

***The above insights make GeeSolver (composed of a ViT encoder and a captcha decoder) outperforms the state-of-the-arts by a large margin.***

## Defense Points

We have reported security issues of text-based captcha to the corresponding company. To defend against our attack, we have also designed two security mechanisms, i.e., the **unpredictable background** and the **overly skewed text**.

### Unpredictable Background (making it difficult for ViT encoder)

Unpredictable background is rarely considered in the existing captcha design. The core of GeeSolver is MAE, which trains the ViT encoder through the reconstruction task of inferring entire characters from their parts. 
After introducing unpredictable backgrounds, MAE will pay much attention to recovering meaningless and complex backgrounds, which has a huge negative impact on the training of the VIT encoder. 
As shown below, we show the reconstructed captchas of MAE using unpredictable backgrounds, more reconstructed cases can be seen in the [reconstructed cases](https://github.com/Anonymous-GeeSolver/GeeSolver/edit/main/DefensePoints). For each triplet, we exhibit the ground truth (top), the masked captcha (middle), and MAE reconstruction (bottom). 
In the case of the same mask, MAE cannot fully recover the captcha characters due to the interference of complex background noise, which indicates that adding unpredictable background can prevent MAE from extracting high-quality representations.
After adding unpredictable backgrounds to Google captchas, the accuracy of GeeSolver drops from 90.7% to 3%. It is worth noting that adding unpredictable backgrounds to existing captchas is simple and will not increase the difficulty of recognition for users.

<div align=center><img src="https://github.com/Anonymous-GeeSolver/GeeSolver/blob/main/DefensePoints/new_captcha_part.jpg" width="950px"></div>

### Overly Skewed Text (making it difficult for captcha decoder) 

Since GeeSolver contains a sequence-based decoder (i.e., left-to-right recognition), overly skewed text will affect performance, which is also proved in the *Microsoft* captchas of dataset A [[1]](https://ieeexplore.ieee.org/document/8327894). GeeSolver only obtains an accuracy of 22.67% when using 500 labeled and 1,000 unlabeled captcha samples. Although the overly skewed text provides a feasible direction to resist the solver attack, it is easily corrected by the preprocessing algorithm. Besides, our solver can still achieve a high success rate (74.76%) with sufficient unlabeled samples (5,000 unlabeled captchas).

<div align=center><img src="https://github.com/Anonymous-GeeSolver/GeeSolver/blob/main/DefensePoints/skewed_captcha.jpg" width="950px"></div>

The overly skewed scheme is selected from the *Microsoft* captcha scheme of dataset A provided by the Tang et al. [[1]](https://ieeexplore.ieee.org/document/8327894) and the conventional scheme is selected from the *Microsoft* captcha scheme of dataset B provided by the Ye et al. [[2]](https://dl.acm.org/doi/10.1145/3243734.3243754).

[1] Mengyun Tang, Haichang Gao, Yang Zhang, Yi Liu, Ping Zhang, and Ping Wang. 2018. [Research on deep learning techniques in breaking text-based captchas and
designing image-based captcha](https://ieeexplore.ieee.org/document/8327894). IEEE Transactions on Information Forensics and Security, vol. 13, no. 10, pp. 2522–2537.

[2] Guixin Ye, Zhanyong Tang, Dingyi Fang, Zhanxing Zhu, Yansong Feng, Pengfei Xu, Xiaojiang Chen, and Zheng Wang. 2018. [Yet another text captcha solver: A
generative adversarial network based approach](https://dl.acm.org/doi/10.1145/3243734.3243754). In Proceedings of the 2018 ACM SIGSAC Conference on Computer and Communications Security (CCS). pp. 332–348.



