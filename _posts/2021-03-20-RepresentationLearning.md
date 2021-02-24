---
layout: post
title: Representation Learning 
---
This blog post covers a talk I gave at the Oxford Machine Learning Summer School 2020 on understanding Representation Learning for Visual Applications

---


This blog covers a talk I gave on Representation Learning for Visual Applications at the Oxford Machine Learning Summer School 2020 in a workshop organised by me and Udit Agarwal. 

The workshop included a talk and a coding session. The coding assignment and it’s solution notebook can be found here: [https://github.com/OxML2020/practicals](https://github.com/OxML2020/practicals)

More about program [https://www.oxfordml.school/](https://www.oxfordml.school/)

The slides to the talk along with all references can be found [here](https://docs.google.com/presentation/d/1ybIi-Rk8yLy63ReW6VuQmysllvf24rGWD4i1mZSg9xY/edit?usp=sharing). The references are not linked here in this post but are in the slides and they are some great ones so do check them out.



---

<font size="6">  What are Representations? </font> 

Representations are concepts. We would like to take in some data in the form of images, text, speech, actions, sensor information or anything really and we want to learn really good concept from them. These concepts are very useful because if we learn good concepts we can ask really good questions about data that we’ve never seen.

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/Intro.png?raw=true" >


For an image we may want to ask: What is in this image? What and where are the objects in this image? How far are things from the camera of this image?
For text we may ask: What would be a possible continuation of this text? What is it's sentiment? What is a summary of it? 

So learning good concept allows us to ask and answer really good questions and that is what reasoning is. If you think about how humans reason, as soon as we look at an image or a piece of text we internally create an understanding of it. Then, once we have created this understanding, we are able to do deductive analysis, ask and answer questions and reason further using this understanding. We almost never reason over raw data, but our representations of it. So good representations are important as we can reason on top of them.

We will gives more examples of computer vision in this talk but also see similar parallels in NLP and other domains. We will talk about some general properties of representation that hold true for text, speech, tabular applications and similar ideas are also used in various control theory applications like AlphaGo as well.



<font size="6"> Why do we need representations? </font> 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/IntroWhyRep.png?raw=true" >

In the first image here we have a 2D matrix and this is how an image is represented to a computer. Its just a matrix of numbers where each number denotes the intensity value at that location. If you animate the intensities it would look like the second figure and to a human it would look like the third.

You can look at the third image and say maybe it is Abraham Lincoln or maybe it is a person but you cannot look at he first and say the same. That is because the contents of the image have nothing to do with the individual pixel values. You are not goning tell me  Abraham Lincoln is in the image because a particular pixel at a certain location has a certain value, you are going to look at the higher-order structure that groups of pixels create that give the image it's meaning. Like groups of pixels make an eye or a noise. These little ideas are what we call representations. We cannot reason over raw pixels generally, we need to convert the raw values of an input into some type of higher order understanding or concept. In this case our brain does this process completely automatically: our eyes record the intensity values of the photons hitting as in the first image, then our visual processing system within our brain creates the image seen in the third and then our prefrontal cortex automatically gives our conscious mind an interpretation/representation of the image. And thus were able to reason about what we see.  

But if all we knew was the first?  Even making a guess would be tuff.


<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/IntroWhyRep2.png?raw=true" >

Trying to get a model to learn good representation is called 'representation learning’ and researchers have been trying to get good at it for decades. Another reason for good representation learning is that image space is not a very ordered space. Let's take a look at these two images. You can see that these two images are very similar in intensity values. We have two people, both of them have their faces approximately in the centre and both of them are wearing dark coloured clothing approximately at the same place. So, if I would represent these two images as a matrix of intensities and then subtract and sum them then I would get a (relatively) low value => if you just look the intensities then these images are very similar. However they contain two different concepts: Pierce Brosnan and Bruce Willis. This third image below is of the same person but has very different intensity values from the other two images. We would get a large value if we subtracted and took the sum. What you're seeing is that even though two pictures of are conceptually very different, they are very close together in pixel intensity space and even though these two images are conceptually the same, they are very far away in pixel intensity space. This means that the space we are dealing with does not naturally represent similarity that we conceptually agree with.

An easy example would be that suppose you are given a graph of certain values like price. As you move away from a certain price like $500 you are getting more and more dis-similar to $500. The more you move away, the more dis-similar you get. You are moving away from $500 not only within that space but also conceptually. Wheras in our image example, even though we were moving very far away from a point within that space, we are conceptually still the same. This means that image space is not an ordered space and these types of spaces are harder to reason over. [comment how cnns turn input to this space]

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/IntroWhyRep3.png?raw=true" >

Another example for color images:
<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/IntroWhyRep4.png?raw=true" >

That is one of our main task with neural networks, to transform our input space into a more ordered space that is easier to reason over. 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/CurseOfDim.png?raw=true" >


There is also the our friend the Curse of Dimensionality. If you think about the possible number of images, its huge. There are billions and gazillions of images possible and there's no way they were going to see all of them in a data set. We have to look at very few images and generalise to the rest. We may look at less than 1% or 0.01 % of natural images, yet they are expected to do well on all of them. In order to do this, we have to learn to exploit certain consistencies that occur within this data type to better design our learning algorithms. 




<font size="6"> How CNNs learn representations </font> 


Let's about the philosophy of CNNs and how they approach the two problems introduced above: the space not being ordered and the curse of dimensionality. CNNs add certain priors which make reasoning over this high dimensional data easier. 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/NN.png?raw=true" >

I’m sure you all have seen this image below of a CNN and what it is supposed to learn at different stages. You have some data set and you can put it into your network and the first few layers are going to learn very local patterns like edges, small circles and small shapes from it. As you move on your network will take these patterns and it is going to form more complex patterns like eyes and lips and facial features. And as you go on you will form even more complex structures that faces. So you have this learning of concepts in a hierarchical manner. This type of hierarchy works well for NLP, speech and other applications as well. The world is compositional: Smaller ideas make up larger ones which make again make up even larger ones and so on. Neural networks leverage this compositionality structure of data.

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/NN2.png?raw=true" >

Let's talk about some assumptions of CNNs through see some examples and then see how those assumption impact the design of networks.
The three key assumptions are Locality, Stationary and Hierarchical. Lets use examples from images and then see examples from other domains.

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/atcod.png?raw=true" >

- **Locality**
 
CNNs assume that features are local. A bird in an image can occur in many different locations, but we don't have to have a different detector for each of those birds. We can just use one detector and apply it to different parts of the image. Objects can appear anywhere and we do not want to link concepts directly to their position. We want to learn features independent of position. These are called spatially independent features. We evaluate things locally, only gradually increasing our receptive field size to look at the bigger picture. What this implies is that patterns exist locally and we just need to look within a local neighbourhood to understand what is present there. 

- **Stationary**
 
There are many patterns that will be repeating throughout natural image space. For example, a dog or a face will occur within millions and gazillions of images so we actually don't need to look at all the possible face images to understand the concept of a face. We can just be look at a thousand and because this this feature is repeating we will capture it in all the million images we haven't seen. Stationary means that feature or representations are repetitive.

- **Hierarchical**

Hierarchical means that concepts are compositional like we spoke about earlier. We could take a large idea like a human body and break the human body into smaller concepts like hands, face and so on. Then we can take one of these concepts, like a face, and break it down to even smaller concepts like eyes, nose and so on. Then we can again take one of these, like eyes, and break It down further to oval, circle, edges etc. Conversely, we can take small structures and concepts and progressively build them into bigger and richer concepts. 



Let's look at some examples at demonstrate these assumptions. 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/Locality.png?raw=true" >

Here, we see that the same bird occurring in different parts of the image. Do we need to look at the entire image to understand a bird is in it? Nope, just a small area.  If we have a detector, is it sensible to learn a different detector for each of these? No right. We want just one detector that we can apply to different parts of the image. 

Lets look at this set of interesting images through the lens of these assumptions. Lets use examples from images and then see examples from other domains.

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/CoolEg1.png?raw=true" >

We can look at each flower in its own local neighbourhood to understand that flower. Similarly, we only need to look in each windows neighbourhood to learn about that window. So even though we're looking at very local regions we can are able to get a good understanding about the contents within that region. This is locality. 
Stationary features are repeating features. In these examples it is very obvious that all of them have repeating elements, these concepts are also repeating throughout our image space. So it doesn't make sense to learn different concepts for each of these as we are seeing just one concept with some variations. Each duck, window and flower has some difference from the rest like it's width, height, angle, color shading etc. It would be very inefficient(and not very smart) if we built an entirely different conceptualisation for a window, a slightly shorter window, a slightly wider window and so on or for a yellow duck at 90 degrees, 89 degrees and so on. Instead it's much more natural(and efficient) to have one concept that can accommodate these variations. So a duck at 60 degrees, 61 degrees.. you get it they’re all the same duck. 

Lastly we can recursively decompose each of these images into smaller concepts. glass->windows->building, leaf->flowers->forest, beak->duck->toy shop?




<font size="6"> Other domain areas </font> 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/CoolEg2.png?raw=true" >

These three properties don’t just occurred in images, they are prevalent in language and sound as well. In language we have words and we use them repeatedly throughout our language(Stationary). Parts of sentences can be understood in isolation(Locality). You could understand a sentence as a standalone sentence, but also in the context of a paragraph and a paragraph in the context of a document and a document within the context of large literature(Hierarchical). Similarly you have a finite number of speech syllables(Stationary) that occur in different positions in words(Locality) and can be combined to create elaborate pronunciations(Hierarchical). In genetic molecules, you have certain repeating molecules(Stationary) like oxygen molecule which can occur in different positions in different places(Locality) and also if you are studying a large molecule that you can look at isolated molecule structure that smaller structures within it and then gather your understanding to understand the whole(Hierarchical). These three properties showing up in different domains and neural networks can be applied where these exist. 

Think and have fun with these properties, they are more prevalent than you may realise! The world is compositional folks.





<font size="6"> Design Implications to CNNs </font> 

Now that we understand these higher level assumptions, lets see how they influence the design of deep neural networks.The Locality assumption directly leads to the concept of weight sharing in CNNs where a filters scans an image for local pattern detection. 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/Compostional1.png?raw=true" >

In order to learn Stationary features we must learn representations which are robust to various transformation and deformations so we do data augmentation to facilitate the learning of such robust filters to generalise to the larger image space. Finally for Hierarchical feature we simply stack many layers to exploit compositional nature of our data. This design helps us overcome curse of dimensionality by using(or exploiting) Locality, Stationary, Hierarchical properties as natural priors in an end-end learnable fashion.





<font size="6"> Learning to Represent </font> 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/Rep3.png?raw=true" >

CNN = Representation Learning + Reasoning

Representation Learning = Shared + Specialised Layers

nitially neutrons detect universally common structures in earlier layers, then they specialise to more class specific structures. Once we obtain these, we can apply our classifier layer or any application head and ask the specific questions we want like where is what in the image. You can read about how neural networks can act as logical gates doing AND,OR and NOT operations on a set of features to create meaningful criterias to evaluate decisions [here](https://bluesky314.github.io/perceptrons/)

We want shared representation before making specialised ones. This thinking stems from the old philosophy of connectionism. Connectionism basically says is that we shouldn't have separate detectors for different things. Before CNNs, people would make separate dog detector and a separate human detector and so on. These detectors would not talk to each other. They were separate models. Connectionism says that if you want really rich and complex understanding, we need to have shared representation among all concepts. And that's basically how these representations get arranged within CNNs.  

CNN = Representation Learning + Reasoning

Representation Learning = Shared + Specialised Layers




<font size="6"> Deep Learning is Representation Learning </font> 

The main point is that in representation learning we are going to take in some raw information like image, text,etc and and turn it into some conceptual features features and then reason over those features. That is what deep learning is. It is representation learning. It is how do we learn good representation over unstructured data. 


<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/APictureIsWorthAThousandWords.png?raw=true" >
A picture is worth a Thousand Words, there are so many details in them and so they always trying to improve our representation learning ability.

Are we done with Conv2ds?
Are Conv2Ds all we need for representation learning?  
Before deep learning we had a bunch of computer vision approaches to solve many tasks and then we started using Conv2Ds. So are we done with representation learning? Or is there also advancements that you can make within deep learning to improve performance.


Lets check on some benchmarks. Benchmarks are a way we can gauge how well our models understand the world by making them do tasks that require real world understanding.

Three common benchmarks in vision are classification, segmentation and detection. Lets see the historical performance of various methods on these applications. 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/Tasks.png?raw=true" >

Lets see the historical performance of various methods on these applications. 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/SOTAclassificaction.png?raw=true" >

Here we can see that the difference in image classification accuracy on ImageNet that between classical CV methods and AlexNet was 13% and the difference from AlexNet to ResNeXt is 25%. So we have almost a double jump within deep learning itself. AlexNet and ResNeXt both have Conv2Ds, but just Conv2Ds are not enough! 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/SOTAseg.png?raw=true" >

A similar pattern in segmentation: classical CV vs FCN: 11% and FCN vs DeepLabV3+ 28%

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/RepLearning/SOTAOD.png?raw=true" >

Likewise for object detection. A huge jump within DL methods. 


The history of deep learning is how can we design our networks to better learn representations and there is much to innovation left for representation learning within in deep learning, today we have attention and transformers slowly taking over the world of vision. But all of them exploit the priors listed here to overcome the curse of dimensionality to learn the best representation they can. For a similar blog post by me please [see](https://bluesky314.github.io/perceptrons/) and do check out the references in the slides for further readings. Thanks for reading.



