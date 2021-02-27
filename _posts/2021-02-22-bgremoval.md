---
layout: post
title: A friendly introduction to Background Removal
---
A friendly introduction to Background Removal and some of it's challenges. The tech used in [EraseBG](https://erase.bg) 

---

&nbsp;

<font size="6"> Section 1: Background Removal and it’s Applications </font> 


Background removal the process of selecting the foreground subject in an image and erasing the background so that the foreground subject can be placed on a completely different background. This is done with help of a mask produced in the removal process as shown below. Placing the subject on a new background is called composition. 


<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/intro.jpg?raw=true" >

As the human eye is very sensitive to discrepancies in images ,delicate care must be taken so that the composition of the extracted subject on a new background looks realistic. This can be tricky for delicate structures like hair and fur. Composition allows us to reuse images by putting them on formal or creative backgrounds. There are two major challenges to creating a completely automated system that can do background removal: 

1) Detecting the foreground subject without any human input: As the foreground subject can belong to a diverse range of objects like humans, animals, electronics, clothings, furnitures etc, our model must correctly identify and handle the subject even if our model has never seen that subject before. Even handling interactions of known subjects, like a human playing basketball or sitting on a chair, can be tricky. 

2) Predicting an accurate mask: The mask must exactly cover only the subject area. Moreover, many structures like fur and human hair have delicate semi-transparent and intricate structures which must be handled with care so that precise extraction and realistic composition can be done.

## Applications


We elaborate more on these challenges in the next section. Let's look at some applications first:

**Reusing photoshoots:** Get more out of our existing content

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/model.jpg?raw=true" >

**Ecommerce:** Get your product images ready and make them seem more appealing for any E-Commerce platform 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/shirt.jpg?raw=true" >
<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/shoe.jpg?raw=true" >


**Media/Creative:** Unfold your creative edge and make stunning content
<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/media.jpg?raw=true" >


**Profile and Passport Pictures:** Create stunning profile pictures in a click. Skip the line and create passport photos anywhere.

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/profilepic.jpg?raw=true" >

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/passport.jpg?raw=true" >


**Logos/Signature/Graphics:** Promote your business or just your cool project

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/graphic.png?raw=true" >

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/sig.jpg?raw=true" >

---


&nbsp;

<font size="6"> Section 2: Why is it hard? </font> 



Our goal is to automatically produce a mask with which we can extract the foreground object from the image. There are two main challenges:

1)Automatically detecting the foreground subject

2)Predicting an accurate mask for realistic composition

While detecting what is the foreground object is easy for a human, it is not so for a computer. In this article we focus our attention on the second challenge and leave the other for a future blog post.

A common approach to generating a mask is a technique called image segmentation which assigns a binary value, a yes or a no, to every pixel in an image to indicate if that pixel belong to the subject or not. Then this mask can be used to extract the object like shown below.

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/solidseg.jpg?raw=true" >


We can see that image segmentation did the job perfectly here. However in more complex cases, such as those with delicate hairs, image segmentation will not do the trick as can be seen below. Even though the mask covers the hair pixels, something is not right in the extraction. This is because the subject, particularly her hair, is semi-transparent at certain locations and interacts with the background's lighting and color  to produce the soft-tone we see in the original image. 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/hairseg.jpg?raw=true" >

In such a case, what we need is a transparency mask or alpha matte like that shown below for proper extraction. Such a mask is able to completely separate foreground and background elements, even at places where they deeply interact.

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/hairalpha.jpg?raw=true" >

The masks created must have a high level of accuracy as compositions created from background removal are often used for ecommerce or media purposes where humans would be seeing them. Lets talk about three factors that impact the realism of compositions: 

* Color decontamination
* Small gaps 
* Alpha blending

&nbsp;

**Color decontamination**

Consider this example to illustrate how slightly different masks can cause big visual differences in composition. On the top is the original image which has a stuffed toy on a bright blue background. Shown below in the first column are two masks generated by two different algorithms. The masks look very similar however when extraction is done using the first, the blue light is still partially visible on the subject’s hair.

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/colorcontamination.png?raw=true" >
- Taken from [A Bayesian Approach to Digital Matting](https://grail.cs.washington.edu/projects/digital-matting/papers/cvpr2001.pdf)

The third column zooms in on a small patch on the right hand side of the toy and we see that the first algorithm slightly over estimated its values leading to more of the background light being taken. Both cover almost the same hair area yet their precise values make a big difference. Algorithms must be able to understand the color and lighting interactions of the foreground and background to circumvent such issues . Even a human would find it hard and time consuming to produce such a mask himself and that’s where background removal comes to the rescue. 

&nbsp;

**Small Gaps**

Even small errors in the mask, such as missing tiny gaps, can cause obvious visual discrepancies when composing on a new background. Below we see the original image on the top and masks produced by two algorithms below. A range of errors in the first mask can be seen. Large gaps like, the one near the shoulder, are obviously visible when the subject is placed on the green background but so are the tiny ones around and within the curly hair. If these gaps are left out then parts of the old background are placed on the new one making the image look synthetic.

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/smallgaps.jpg?raw=true" width="450" height="570" >

&nbsp;

**Alpha blending**

Lets see how our transparency mask promote realistic composition. Our transparency mask indicates for every pixel how much of the foreground and background colours should be present. For certain pixel we would have a blend of foreground and background colours like 60% foreground and 40% background. Such blending makes it appear as if the subject were truly present in the new background and interacting with the lightning there. Compositions also seem less jaggy around edges and more natural and appealing to the human eye. 

Below, in c) is a small patch of brown hair extracted from the stuffed toy above which we are trying to compose on the very bright background in a) for illustration. The colourful background is multiplied with the inverted mask of our subject and combined with the extracted hair to produce the composition as seen in d). As the patch is from a semi-transparent region there is a lot of interaction with the background colours. In d) we see how this blending technique produces a mixture of colours making it appear as if the subject were present to be interacting with the lightning of the new background. There are more advanced techniques for composing subjects and backgrounds from very different lighting conditions but we do not discuss them here.

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/compositionzoom.png?raw=true" >
- Taken from Computer Vision and Algorithms and Applications by Richard Szeliski

&nbsp;

In conclusion we saw that background removal is a delicate process that requires transparency prediction to get right. Using the map generated in the removal process we are able to extract the subject and compose to a new background. We spoke of three important considerations that affect realism of the compositions and the level of accuracy and detail expected from algorithms that attempt to produce these masks. We hope enjoyed reading this article and now have a deeper appreciation of background removal and its many applications. To see all this in action try out our background remover [EraseBG](https://erase.bg). Offical upgraded launch date 10th March.

