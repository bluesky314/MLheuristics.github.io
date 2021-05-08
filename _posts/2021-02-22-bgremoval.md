---
layout: post
title: A friendly introduction to Background Removal
---
A friendly introduction to Background Removal and some of it's challenges. The tech used in [EraseBG](https://erase.bg) 

---

&nbsp;

<font size="6"> Section 1: Background Removal and it’s Applications </font> 


Background removal is the process of selecting the foreground subject in an image and erasing the background so that the foreground subject can be placed on a new background. This is done with the help of a mask produced in the removal process as shown below. Placing the subject on a new background is called composition.


<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/intro.jpg?raw=true" >

As the human eye is very sensitive to discrepancies in images, great care must be taken so that the composition of the extracted subject looks realistic on a new background. This can be tricky for delicate structures like hair and fur. Composition allows us to reuse images by putting them on formal or creative backgrounds. There are two major challenges in creating a completely automated system that can do background removal:

1) Detecting the foreground subject without any human input: As the foreground subject can belong to a diverse range of objects like humans, animals, electronics, clothing, furnitures etc., our model must identify and handle the subject even if our model has never seen that subject before. Handling interactions of known subjects, like a human playing basketball or sitting on a chair, can also be tricky.

2) Predicting an accurate mask: The mask must exactly cover only the subject area. Moreover, many structures like fur and human hair have delicate semi-transparent and intricate structures which must be handled with care so that precise extraction and realistic composition can be done.

## Applications


In the next section, we will elaborate more on these challenges and show examples to explain them in detail. For now, let’s look at some applications:

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

<font size="6"> Section 2: Challenges </font> 



Our goal is to automatically produce a mask to extract the foreground object from the image. There are two main challenges in doing this:

1)Automatically detecting the foreground subject

2)Predicting an accurate mask for realistic composition

While detecting what is the foreground object is easy for a human, it is not so for a computer. In this post we focus our attention on the second challenge and leave this one for a future blog post.

A common approach to generating a mask is a technique called **image segmentation** which assigns a binary value, a YES or a NO, to every pixel in an image to indicate if that pixel belong to the subject or not. Then, this mask can be used to extract the object as shown below.

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/solidseg.jpg?raw=true" >

We can see that image segmentation did the job perfectly here. However, in more complex cases, such as those with delicate hairs, image segmentation will not do the trick as seen below. Even though the mask covers the hair pixels, something is not right in the extraction. This is because part of the subject, particularly her hair, is semi-transparent at certain places and interacts with the lighting and color of the background to produce the soft-tone we see in the original image.

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/hairseg.jpg?raw=true" >

In such a case, what we we need is a **transparency mask** or **alpha matte** for proper extraction as that shown below. Such a mask can completely separate foreground and background elements, even at places where they deeply interact.

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/hairalpha.jpg?raw=true" >

The created masks must have a high level of accuracy as compositions created from background removal are often used for ecommerce or media purposes where humans would be seeing them. Lets talk about three factors that impact the realism of compositions:

* Color decontamination
* Small gaps 
* Alpha blending

&nbsp;

**Color decontamination**

Consider the below example to illustrate how slightly different masks can cause significant visual differences in composition. The top image is the original image which has a stuffed toy on a bright blue background. Shown below it in the first column are two masks generated by two different algorithms. The masks look very similar; however when extraction is done using the first, the blue light is still partially visible on the subject’s hair as shown in the second column.

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/colorcontamination.png?raw=true" >
- Taken from [A Bayesian Approach to Digital Matting](https://grail.cs.washington.edu/projects/digital-matting/papers/cvpr2001.pdf)

In the third column, we can see close ups of a small patch on the right-hand side of the toy. Here, we notice that the first algorithm has slightly over estimated its values leading to more of the background light being taken in the extraction. Both cover almost the same hair area, yet their precise values make a big difference. Algorithms must understand the colours and lighting interactions of the foreground and background to circumvent such issues . Even a human would find it difficult and time consuming to produce such a mask himself, and that’s where background removal comes to the rescue.

&nbsp;

**Small Gaps**

Even small errors in the mask, such as missing tiny gaps, can cause obvious visual discrepancies when composing on a new background. Below we see the original image on the top and masks produced by two algorithms on the right.

A range of errors in the first mask are visible. Large gaps like the one near the shoulder are clearly visible when the subject is placed on the green background, but so are the tiny ones around and within the curly hair. If these gaps are left out then parts of the old background are placed on the new one making the image look synthetic.

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/smallgapsv2.jpg?raw=true" width="800" height="500" >

&nbsp;



**Alpha blending**

Let’s see how our transparency mask promote realistic composition. Our transparency mask indicates how much of the foreground and background colours should be present for every pixel. For example, at a certain pixel we could have a blend of 60% foreground colour and 40% background colour. Such blending makes it appear as if the subject was truly present in the new background and interacting with the lightning there. Compositions also seem less jaggy around edges and more natural and appealing to the human eye.

When composing, we don’t want the background to abruptly start. We want a smooth transition from the foreground subject to background region. To illustrate, we compose a small patch of brown hair extracted from the corner of the stuffed toy above in c) on the bright background in a) below. When we blend with the help of our mask in b) we see a smooth transition and interaction of colours in the composition produced in d) making it appear as if the subject was actually present and interacting with the lightning of the new background. There are more advanced techniques for composing subjects and backgrounds from different lighting conditions but we do not discuss them here.

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/bgremoval/compositionzoom.png?raw=true" >
- Taken from Computer Vision and Algorithms and Applications by Richard Szeliski

&nbsp;

In conclusion we saw that background removal is a delicate process that requires transparency prediction to get right. Using the map generated in the removal process , we are able to extract the subject and compose on a new background. We spoke of three important considerations that affect the realism of the compositions and the level of accuracy and detail expected from algorithms that attempt to produce these masks.

We hope you enjoyed reading this blog and now have a deeper appreciation of background removal and its many applications. To see all this in action, try out our background remover EraseBG that is set to launch with a new website on 30th May 2021.
