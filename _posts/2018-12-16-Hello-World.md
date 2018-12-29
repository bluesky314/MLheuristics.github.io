---
layout: post
title: A brief Introduction to SSIM: Structural Similarity Index
---
A brief Introduction to SSIM: Structural Similarity Index

---
This is a blog on SSIM that I had written some time back and saved as a pdf. You can find the blog [here](https://drive.google.com/file/d/1rM3fMJ45F-bVYSz7dL8y1_mBDChIrs8g/view?usp=sharing)

I will briefly introduce the importance of the topic here: 

The SSIM index is used for measuring the similarity between two images. The SSIM
predicts image quality based on an initial uncompressed or distortion-free image as reference. It
tells us how far away an image is from its original reference image more aligned with the human

perceptual system. SSIM is designed to improve on traditional methods such as peak signal-to-
noise ratio (PSNR) and mean squared error. The is a very important concept in digital signal processing and comes in handy in applications of deep learning as well. Surprisingly I have seen
very few posts about this metric so decided to write a approachable explanation for this.
As can be seen above, the MSE is not the most accurate measurement of distortions to an image
as they appear to our human eyes. For this we define a more holistic metric which considers three
key components of our visual system.

