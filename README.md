# p2p-editing: Child face generation form two parents' images based on pixel2style2pixel (pSp, a StyleGAN encoder)

## 概要
pixel2style2pixel（略pSp） encoderを使い、親の顔写真から、親の顔のlatent vectorsを出して結合する。  
そして、結合されたlatent vectorから、子供の顔写真を生成できる。  

例として、下記の２つの顔写真をpSp encoderに入力する。　　

<img src="https://github.com/jiangjw88/p2p-editing/blob/master/images/HG_ali.png" width="200" height="200" alt=""/><img src="https://github.com/jiangjw88/p2p-editing/blob/master/images/LSS_ali.png" width="200" height="200" alt=""/>　　

出力として２つのlatent vectorsを得る。  
また、得られたlatent vectorsをeditingsの[latent_editor.py](https://github.com/jiangjw88/p2p-editing/blob/master/editings/latent_editor.py)とmodelsの[psp.py](https://github.com/jiangjw88/p2p-editing/blob/master/models/psp.py)に通し、入力された顔写真を再現する。  

<img src="https://github.com/jiangjw88/p2p-editing/blob/master/images/parents.png" width="400" height="200" alt=""/>  

最後、上記の２つの顔写真から得たlatent vectorsを結合して（ここでは算数平均を取る）[latent_editor.py](https://github.com/jiangjw88/p2p-editing/blob/master/editings/latent_editor.py)とmodelsの[psp.py](https://github.com/jiangjw88/p2p-editing/blob/master/models/psp.py)に通し、入力顔写真の2人の子供の顔写真を得る（下記左写真）。また、下記右写真は年齢を調整しないまま、得たものである。  

<img src="https://github.com/jiangjw88/p2p-editing/blob/master/images/HG%26LSS_Child.png" width="400" height="200" alt=""/>  


## Motivation
In order to know the appearance of the child, I thought of extracting the characteristics of their parents' appearance, combining them( in some way), and then obtaining the characteristics of their child, which could be used for generating the image of their child.

## Pretained model 
At first, I used the pretrained pSp model, including the encoder and decoder weights.
The model was trained with the FFHQ dataset by eladrich, and we can download it from path [StyleGAN Inversion](https://drive.google.com/file/d/1bMTNWkh5LArlaWSc_wa8VKyq2V42T2z0/view?usp=sharing).

## Create child face image
Step 1: Extract the latent spaces from two parents' face image by using pretrained pSp encoder.  
Step 2: Simply taking the average of the parents’ latent spaces, moving negatively in the ‘age direction’, and moving randomly in the ‘gender direction’.  
Step 3: Generate child face image from the average latent space by using pretrained pSp decoder.

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
[encoder4editing](https://github.com/omertov/encoder4editing).

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

```
