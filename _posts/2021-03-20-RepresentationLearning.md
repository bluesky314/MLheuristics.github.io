---
layout: post
title: Representation Learning for Visual Applicatioons
---
This is a blog post covering the contents of a workshop organised at the Oxford Machine Learning Summer School 2020 by me and Udit Agarwal on understanding Representation Learning

---



This is a blog post covering the contents of a workshop organised at the Oxford Machine Learning Summer School 2020 by me and Udit Agarwal. The workshop included one lecture and a practical coding session on Representation Learning for Visual Applications.


The coding assignment and it’s solution notebook can be found here: https://github.com/OxML2020/practicals
The slides to the talk along with all references can be found here: 
A video of the talk will soon be available. 

 

What are Representations? Representations are basically concepts. We want to take in some data type like images, text, speech, actions, sensor information or anything really and we want to learn really good concept from them. These concepts are very useful because if we learn good concepts we can ask really good questions.
Then we can ask and answer really good questions about data that we’ve never seen that is of the same type.

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/Intro.png?raw=true" >


From an image we may want to ask: What is in this image? What and where are the objects in this image? How many of something is in this image?
For text we may ask: What is the emotion of this text? What is a summary of it? What is a good continuation of this text?

So learning good concept allows us to ask really good questions and that is what reasoning is. If you think about how humans reason, when we look at an image or when we look at a piece of text we internally create an understanding of it. Then, once we have created that understanding, we are able to do deductive analysis, ask and answer questions and reason further using this understanding. We almost never reason over raw data, but our representations of it. So good representations are really very important for reasoning.

We will focus more on computer vision (and nlp)but we will talk about some general properties of representation that would allow was to also understand text, speech and tabular applications and similar ideas are also used in various control theory applications like AlphaGo.



Why do we need representations?
<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/IntroWhyRep.png?raw=true" >

Here you can see we have a 2d matrix and this is how an image is represented to a computer. Its just a matrix of numbers where each number denotes its intensity values. If you animate the intensities it would look like b) and to a human it would look like c)

You can look at this image c) and say maybe it is Abraham Lincoln or maybe it is a person but you cannot look at a) and say the same. That is because the contents of the image has nothing to do with the individual pixel values. You are not gonna tell me its because a particular pixel at a certain location has a certain value, you are going to look at the higher-order structure that the pixels create that give the image it's meaning. 
We cannot reason over raw pixels generally, we need to convert the raw values into some type of higher order understanding or concept. In this case our brain does this process completely automatically: our eyes record the intensity values of the photons hitting as in a) our visual processing system within our brain creates the image seen in c) and prefrntex cortex just gives our conscious mind an interpretation of it involuntarily. And thus were able to reason about what we see.  
But if we were just given a) the reasoning would be would be very difficult. 
