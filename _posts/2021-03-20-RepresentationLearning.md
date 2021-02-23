---
layout: post
title: Representation Learning for Visual Applicatioons
---
This blog post covers the contents of a workshop organised by me and Udit Agarwal at the Oxford Machine Learning Summer School 2020 on understanding Representation Learning

---



This blog post covers the contents of a workshop organised by me and Udit Agarwal at the Oxford Machine Learning Summer School 2020. The workshop included one lecture and a practical coding session on Representation Learning for Visual Applications.


The coding assignment and it’s solution notebook can be found here: https://github.com/OxML2020/practicals

The slides to the talk along with all references can be found here: 

A video of the talk will soon be available. 

---

**What are Representations?**

Representations are basically concepts. We want to take in some data type like images, text, speech, actions, sensor information or anything really and we want to learn really good concept from them. These concepts are very useful because if we learn good concepts we can ask really good questions.
Then we can ask and answer really good questions about data that we’ve never seen that is of the same type.

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/Intro.png?raw=true" >


From an image we may want to ask: What is in this image? What and where are the objects in this image? How many of something is in this image?
For text we may ask: What is the emotion of this text? What is a summary of it? What is a good continuation of this text?

So learning good concept allows us to ask really good questions and that is what reasoning is. If you think about how humans reason, when we look at an image or when we look at a piece of text we internally create an understanding of it. Then, once we have created that understanding, we are able to do deductive analysis, ask and answer questions and reason further using this understanding. We almost never reason over raw data, but our representations of it. So good representations are really very important for reasoning.

We will focus more on computer vision (and nlp)but we will talk about some general properties of representation that would allow was to also understand text, speech and tabular applications and similar ideas are also used in various control theory applications like AlphaGo.



**Why do we need representations?**

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/IntroWhyRep.png?raw=true" >

Here you can see we have a 2d matrix and this is how an image is represented to a computer. Its just a matrix of numbers where each number denotes its intensity values. If you animate the intensities it would look like b) and to a human it would look like c)

You can look at this image c) and say maybe it is Abraham Lincoln or maybe it is a person but you cannot look at a) and say the same. That is because the contents of the image has nothing to do with the individual pixel values. You are not gonna tell me its because a particular pixel at a certain location has a certain value, you are going to look at the higher-order structure that the pixels create that give the image it's meaning. 
We cannot reason over raw pixels generally, we need to convert the raw values into some type of higher order understanding or concept. In this case our brain does this process completely automatically: our eyes record the intensity values of the photons hitting as in a) our visual processing system within our brain creates the image seen in c) and prefrntex cortex just gives our conscious mind an interpretation of it involuntarily. And thus were able to reason about what we see.  
But if we were just given a) the reasoning would be would be very difficult. 


<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/IntroWhyRep2.png?raw=true" >

Another reason for good representation learning is that image space is not a very ordered space. Let's take a look at these two images. You can see that these two images are very similar in intensity values. We have two people, both of them have their faces approximately in the centre and both of them are wearing a dark coloured clothing approximately at the same place. So, if I would represent these two images as a matrix of intensities and then subtract and sum them then, I would get a (relatively) low value. Which is because if you just look the intensities then these images are very similar. This third image is of the same person but has very different intensity values. We would get a large value if we subtracted and took the sum. What you're seeing is that even though these two pics are conceptually very different, they are very close together in pixel intensity space and even though these two images are conceptually the same, they are very far away in pixel intensity space. This means that the space we are dealing with does not represent similarity that we conceptually agree with[more explanation]

An easy example would be that suppose you are given a graph of certain values like price. As you move away from a certain price like $500 you are getting more and more dis-similar to $500. The more you move away, the more dis-similar you get. You are moving away from $500 within that space[graph?] and also conceptually. Wheras in our image example, even though we were moving very far away from a point we  are still conceptually the same. This means that image space is not an ordered space and these types of spaces are harder to reason over. [comment how cnns turn input to this space]

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/IntroWhyRep3.png?raw=true" >

Another example for color images:
<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/IntroWhyRep4.png?raw=true" >

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/CurseOfDim.png?raw=true" >
There is also the our friend the Curse of Dimensionality. If you think about the possible number of images, its huge. There are millions and millions of images possible and there's no way they were going to see all of them in a data set. We have to look at very few images and generalized to the rest. We may look at less than 1% or 0.01 % of natural images yet they are expected to do well on all of them.
In order to do this, we have to learn to exploit certain consistencies that occur within this data type which will allow us to in a better design our learning algorithms. 


**How cnns learn representations**

We will talk about the philosophy of CNN and how the to approach the two problem introduced above. CNNs basically add certain priors which will make reasoning over this high dimensional data easier. 
<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/NN.png?raw=true" >
I’m sure you all have seen this image of a CNN and what is supposed to learn at different stages. So over here you have some data set and you can put it into your network and the first few layers are going to learn very local patterns like edges, small circles and small shapes from it. As you move on your network will take these patterns and it is going to form more complex patterns like eyes and lips and facial features. And as you go on you will form even more complex structures that faces. So you have this learning concepts in hierarchical manner. 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/NN2.png?raw=true" >

Let's talk about some assumptions of CNNs through see some examples and then see how those assumption impact the design of networks.
The three key assumptions are Locality, Stationary and Hierarchical. Lets use examples from images and then see examples from other domains.
Define ‘feature’?

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/atcod.png?raw=true" >

- Locality
Cnns assume that features are local. A bird in an image can occur in many different locations, but we don't have to have a different detector for each of those birds. We can just use one detector and apply i to different parts of the image. Objects can appear anywhere and we do not want to link features/concepts directly to the position. We want to learn features not dependent on position. These can called spatially independent features. What this implies is that pattern exist locally and we just need to look within a local neighborhood to understand what is present there. 

- Stationary
We spoke about things within an image but there are certain patterns that will be repeating throughout our natural image space. For example, dog or a face will occur within millions of times so we actually don't need to look at all the possible face images to understand the concept of a face. We can just be look at a thousand and because this this feature is repeating we will capture it in all the million images I haven't seen.

- Hierarchical
Hierarchical means that concepts are compositional. We could take a large idea like a human body and break the human body into smaller concepts like hands, face and so on. Then we can take one of these concepts, like a face, and break it down to even smaller concepts like eyes, nose and so on. ThenweI can again take one of these, like eyes, and break It down further to oval, circle, edges etc. Conversely, we can take small structures and concepts and progressively build them into bigger and richer concepts. 


Let's look at some examples at demonstrate these assumptions. 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/Locality.png?raw=true" >

Here, we see the same bird occurring in different parts of the image. If we have a detector, is it sensible to learn a different detector for each of these? No right. We want just one detector that we can apply to different parts of the image. This example displays locality, the patterns of the bird exist locally and we only need to look at local regions to evaluate. [Maybe talk of moving the detection across the grid][can talk about NLP, sequential processing there makes this seem more natural] 

Lets look at this set of interesting images through the lens of these assumptions. Lets use examples from images and then see examples from other domains.
<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/CoolEg1.png?raw=true" >
We can look at each flower in its own local neighbourhood to understand that flower. Similarly, we only need to look in each windows neighbourhood to learn about that window. So even though we're looking at very local regions we can are able to get a good understanding about the contents within that region. This is locality. 
Stationary features are repeating features. In these examples it is very obvious that all of them have repeating elements, these concepts are also repeating throughout our image space. So it doesn't make sense to learn different concepts for each of these as we are seeing just one concept with some variations. Each duck, window and flower has some difference from the rest like it's width, height, angle, color shading etc. It would be very inefficient(and dumb) if we built an entirely different conceptualisation for a window, a slightly shorter window, a slightly wider window and so on or for a yellow duck at 90 degrees, 89 degrees and so on. Instead it's much more natural(and efficient) to have one concept that can accommodate these variations. So a duck at 60 degrees, 61 degrees.. you get it they’re all the same duck. 

Lastly we can recursively decompose each of these into smaller concepts. glass->windows->building, leaf->flowers->forest, beak->duck->toy shop?

Lets look at other domain areas now
<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/CoolEg2.png?raw=true" >

These three properties that we spoke of don’t just occurred in images, they are prevalent in language and sound as well. In language we have words and we use them repeatedly throughout our language(Stationary) and we also place them in different places in sentences(Locality). You can understand a sentence as a standalone sentence, but you can also understand it in the context of a paragraph and you can understand a paragraph in the context of a document or a document within the context of large literature(Hierarchical). Similarly you have a finite number of speech syllables(Locality) that occur in different positions in words(Stationary) and can be combined to create elaborate pronunciations(Hierarchical). In genetic molecules, you have certain repeating molecules(Stationary) like oxygen molecule which can occur in different positions in different places(Locality) and also if you are studying a large molecule that you can look at isolated molecule structure that smaller structures within it and then gather your understanding to understand the whole(Hierarchical). These three properties showing up in different domains and neural networks can be applied where these exist. 

The World is Compositional.
The world as being made out of a fundamental units and we can accumulate the fundamental units to form higher-order concepts.


**Design Implications to CNNs**

Now that we understand these higher level assumptions, lets see how they influence the design in deep neural networks.
Locality assumption directly leads to the concept of weight sharing in CNNs where a filters scans an image for local pattern detection.
You can see that this pattern is a repeating and a detector should be able to evaluate all of these four so basically we want the same network parameters to detect patterns at many different positions. [unlike fc: biased to location][Show e.g. of how an edge filer works across location]

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/Compostional1.png?raw=true" >

In order to learn stationary features we must learn representations which are robust to various transformation and deformations so we do data augmentation to facilitate the learning of such robust filters to generalise to the larger image space.
Hierarchy: Many layers 
Stacking many layers to exploit compositional nature of our data.

These help us overcome curse of dimensionality. CNNs exploit Local,stationary, Hierarchy in an end-end learnable fashion.


**Learning to Represent**

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/Rep3.png?raw=true" >

CNN = Representation Learning + Reasoning
Representation Learning = Shared + Specialised Layers

Initially neutrons detect universally common structures in earlier layers, then they specialise to more class specific structures. Once we obtain these, we can apply our classifier layer or any application head and ask the specific questions we want like where is what in the image. [Connectionism]
(Head as reasoning)

We want shared representation before making specialised ones. This thinking stems from the old philosophy of connectionism. Connectionism basically says is that we shouldn't have separate detectors for different things. Before CNNs, people would make separate dog detector and a separate human detector and so on. These detectors would not talk to each other. They were separate models. Connectionism says that if you want really rich and complex understanding, we need to have shared representation among all concepts. And that's basically how these representations get arranged within CNNs. 

CNN = Representation Learning + Reasoning
Representation Learning = Shared + Specialised Layers

Quick points:
....


**Deep Learning is Representation Learning**

The main point is that in representation learning we are going to take in some raw information like image, text,etc and and turn it into some conceptual features features and then reason over those features. That is what deep learning is. It is representation learning. It is how do we learn good representation over unstructured data. 


<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/APictureIsWorthAThousandWords.png?raw=true" >
A picture is worth a Thousand Words, there are so many details in them and so they always trying to improve our representation learning ability.

Are we done with Conv2ds?
Before deep learning we had a bunch of computer vision approaches to solve many tasks and then we started using conv2ds. So are we done with representation learning? Or is there also advancements that you can make within deep learning to improve performance.

Lets check on some benchmarks,  benchmarks are a way we can gauge how well our models understand the world by making them do tasks that require real world understanding.
Three common benchmarks in vision are classification, segmentation and detection.
<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/Tasks.png?raw=true" >

Lets see the historical performance of various methods on these applications. 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/SOTAclassificaction.png?raw=true" >
<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/SOTAseg.png?raw=true" >
<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/SOTAOD.png?raw=true" >



