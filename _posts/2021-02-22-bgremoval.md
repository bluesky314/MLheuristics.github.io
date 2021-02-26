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

 
