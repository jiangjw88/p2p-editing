# p2p-editing: Child face generation form two parents' images based on pixel2style2pixel (pSp, a StyleGAN encoder)

## Motivation
In order to know the appearance of the child, I thought of extracting the characteristics of their parents' appearance, combining them( in some way), and then obtaining the characteristics of their child, which could be used for generating the image of their child.

## Pretained model 
At first, I used the pretrained pSp model, including the encoder and decoder weights.
The model was trained with the FFHQ dataset by eladrich, and we can download it from path [StyleGAN Inversion](https://drive.google.com/file/d/1bMTNWkh5LArlaWSc_wa8VKyq2V42T2z0/view?usp=sharing).

## Create child face image
Step 1: Extract the latent spaces from two parents' face image by using pretrained pSp encoder.
Step 2: Simply taking the average of the parents’ latent spaces, moving negatively in the ‘age direction’, and moving randomly in the ‘gender direction’.
Step 3: Generate child face image from the average latent space by using pretrained pSp decoder.


## Training encoder for Asian faces (still working on it)
In this repository, I provide pretrained ReStyle encoder applied over the 
[pSp](https://github.com/eladrich/pixel2style2pixel), using the lite version dataset of The Asian Face Age Dataset([AFAD-LITE](https://github.com/afad-dataset/tarball-lite)).



## Credits
**StyleGAN2 model and implementation:**  
https://github.com/rosinality/stylegan2-pytorch  
Copyright (c) 2019 Kim Seonghyeon  
License (MIT) https://github.com/rosinality/stylegan2-pytorch/blob/master/LICENSE  

**pSp model and implementation:**   
https://github.com/eladrich/pixel2style2pixel  
Copyright (c) 2020 Elad Richardson, Yuval Alaluf  
License (MIT) https://github.com/eladrich/pixel2style2pixel/blob/master/LICENSE

**e4e model and implementation:**   
https://github.com/omertov/encoder4editing
Copyright (c) 2021 omertov  
License (MIT) https://github.com/omertov/encoder4editing/blob/main/LICENSE

**The Asian Face Age Dataset (AFAD):**    
https://github.com/afad-dataset/tarball-lite

**Please Note**: The CUDA files under the [StyleGAN2 ops directory](https://github.com/eladrich/pixel2style2pixel/tree/master/models/stylegan2/op) are made available under the [Nvidia Source Code License-NC](https://nvlabs.github.io/stylegan2/license.html)

## Acknowledgments
This code borrows heavily from [pixel2style2pixel](https://github.com/eladrich/pixel2style2pixel),
[encoder4editing](https://github.com/omertov/encoder4editing), and
[restyle-encoder](https://github.com/yuval-alaluf/restyle-encoder).

## Citation
If you use this code for your research, please cite the following works:
```
@InProceedings{richardson2021encoding,
      author = {Richardson, Elad and Alaluf, Yuval and Patashnik, Or and Nitzan, Yotam and Azar, Yaniv and Shapiro, Stav and Cohen-Or, Daniel},
      title = {Encoding in Style: a StyleGAN Encoder for Image-to-Image Translation},
      booktitle = {IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)},
      month = {June},
      year = {2021}
}
@article{tov2021designing,
      title={Designing an Encoder for StyleGAN Image Manipulation},
      author={Tov, Omer and Alaluf, Yuval and Nitzan, Yotam and Patashnik, Or and Cohen-Or, Daniel},
      journal={arXiv preprint arXiv:2102.02766},
      year={2021}
}
@InProceedings{alaluf2021restyle,
      author = {Alaluf, Yuval and Patashnik, Or and Cohen-Or, Daniel},
      title = {ReStyle: A Residual-Based StyleGAN Encoder via Iterative Refinement}, 
      month = {October},
      booktitle = {Proceedings of the IEEE/CVF International Conference on Computer Vision (ICCV)},  
      year = {2021}
}

```
