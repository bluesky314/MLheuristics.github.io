---
layout: post
title: A friendly introduction to Background Removal
---
A friendly introduction to Background Removal and thoughts that went into creating Erase.BG

---


**Section 1: Introduction. What is background removal?**

Background removal the process of selecting the foreground subject in an image and erasing the background so that the foreground subject can be placed on a completely different background. This is done with help of a mask produced in the removal process as shown below. Placing the subject on a new background is called composition. 


<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/intro.jpg?raw=true" >

As the human eye is very sensitive to discrepancies in images ,delicate care must be taken so that the composition of the extracted subject on a new background looks realistic. This can be tricky for delicate structures like hair and fur. Composition allows us to reuse images by putting them on formal or creative backgrounds. There are two major challenges to creating a completely automated system that can do background removal: 

1) Detecting the foreground object without any human input: As the foreground subject can belong to a diverse range of objects like humans, animals, electronics, clothings, furnitures etc, our model must correctly identify and handle the object even if our model has never seen the object before.

2) Predicting an accurate mask for extraction: The mask must exactly cover only the subject area. Moreover, many structures like fur and human hair have complicated and delicate semi-transparent structures which must be handled with care for precise extraction and realistic composition.

We elaborate more on these challenges in the new section. Here we present some applications:

**Reusing photoshoots**: Get more out of our existing content

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/model.jpg?raw=true" >

**Ecommerce**: Get your product images ready instantly for any eCommerce platform

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/shirt.jpg?raw=true" >
<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/shoe.jpg?raw=true" >


**Media/Creative**: Unfold your creative edge and make stunning content
<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/media.jpg?raw=true" >


**Profile and Passport Pictures**: Create stunning profile pictures in a click. Skip the line and create passport photos anywhere.

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/profilepic.jpg?raw=true" >

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/passport.jpg?raw=true" >


**Logos/Signature/Graphics**: Works on graphic arts and signatures 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/graphic.png?raw=true" >

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/sig.jpg?raw=true" >

 
**Section 2: Why is it hard?**

Our goal is to automatically produce a mask with which we can extract the foreground object from the image as shown in below. There are two main challenges:

1)Automatically detecting the foreground object. 

2)Predicting a extremely accurate mask for realistic composition.

While detecting what is the foreground object is easy for a human it is not so for a computer. In this article we do not delve into this and elaborate on the second challenge.

A common approach to generating a mask is a technique called image segmentation which assigns a binary value, a yes or a no, to every pixel in an image to indicate if that pixel belong to the subject or not. Then this mask can be used to extract the object like shown below.

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/solidseg.jpg?raw=true" >


We can see that image segmentation did the job perfectly here. However in more complex cases, such as those with delicate hairs, image segmentation will not do the trick as can be seen in fig 2. Even though the mask covers the hair pixels, something is not right in the extraction. This is because the subject, particularly her hair, is semi-transparent at certain locations and interacts with the background's lighting and color  to produce the colour and soft-tone we see in the original image. 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/hairseg.jpg?raw=true" >

In such a case we create a transparency mask like that shown below for proper extraction of the subject. Such a mask is able to completely separate foreground and background elements, even at places where they deeply interact.

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/hairalpha.jpg?raw=true" >


The masks created must have a high level of accuracy as image created from background removal are often used for ecommerce or media purposes where humans would be seeing them. Lets talk about three factors that impact the realism of compositions: color decontamination, small gaps and fg/bg blending.

**Color decontamination**

Consider this example to illustrate how slightly different masks can cause big visual differences. The original image has a stuffed toy on a bright blue background and shown below it are two masks generated from two different algorithms. The masks look very similar however when extraction is done using the first, the blue light is still partially visible on the subject’s hair. 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/colorcontamination.png?raw=true" >
- https://grail.cs.washington.edu/projects/digital-matting/papers/cvpr2001.pdf

As can be seen in the third column, the first algorithm slightly over estimates the opacity values leading to more of the background light being taken. Our methods need to be extremely precise to circumvent this issue . Even a human would find it very hard to produce this mask himself. The algorithm must be able to understand the color and lighting interaction of the background and foreground to produce a mask without colour spilling.


**Small Gaps**

Even small errors in the mask, such as missing tiny gaps can cause large/obvious visual dispecency when composing on a new background as shown above. If any of the tiny gaps are left out then the compose still contains the white wall color from the previous background making it look unrealistic.  

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/smallgaps.jpg?raw=true" width="495" height="630" >
