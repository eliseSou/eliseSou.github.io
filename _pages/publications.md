---
layout: archive
title: "GIST Final report"
permalink: /gist_final_report/
author_profile: false
---

Data Engineering course : Team 9 final Project, Apple sweetness finder
======================================================
 Welcome ! This is the final report of team 9 as part of GIST Data Engineering course. The aim was to developp a ML project with a buiseness objectif. 
 You can find the git repository [here](https://github.com/eliseSou/apple_swetness_finder).

The Team 
----------------
First let me introduce our team : 
+ Junsik Kim
+ Hyungseok Ryu
+ Youngin Choi
+ Elise Souvannavong

Problem Definition
-------------

After brainstorming together we came up with a few ideas: text summarizer for college students, AND AFTER I DON’T REMEMBER. But eventually, we choose to develop a model which could predict the sweetness of apples based on pictures. We wanted to create a project which could be useful in everyday life with direct application. 
As of today, to predict the sweetness of fruit there is one solution: the refractometer. A refractometer is a small tool, on which you are supposed to put a few drops of the product you want to measure and then you will see the sugar level in terms of percentage. In reality, this tool measures the refraction of the juice, which is influenced by the level of sugar. This method is the most accurate way, but it requires breaking the fruit every time, thus making it unusable while grocery shopping. 

Indeed, our goal was to create a simple application which you could use on your phone to choose the best fruit possible.  Moreover, the colour of a fruit is correlated to its sugar level, which is why we believe that is possible to predict a fruit’s sweetness based on a simple photo. However machine learning is as powerful as the dataset let it be, so we were limited by available datasets, hence why we choose to develop this project for apples only. You can find the original dataset [here](https://www.aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100&aihubDataSe=realm&dataSetSn=490).




System Design
-------------

To make our project work we needed machine learning model which could detect apples and predict their sweetness, a server to host the trained model and the dataset, and a client-side application which could take pictures as input and communicate with the server. 
To implement all that, we chose to host 

### Training server

The goal of this server was to host all the dataset and then train the model with GIST's CPU. 

### Streamlit and Webserver

At first we wanted to create a web application, 

### Mobile phone application 


Machine Learning component 
----------------

To achieve our goal we needed a model capable to detect many apples in a frame, and then applying regression based on the detected apples to predict their sweetness level.


### YOLO model 

For the backbone model, we chose to use a pre-trained YOLO model. We choose this model because it can do at the same time object segmentation and object classification. 
After a few trials with different versions, we concluded that YOLOv5 was the most efficient for our project. 

Then we trained it with the appel dataset and evaluated it through our laptop webcam with pictures from the dataset and real apples. We noticed some problems in different cases, for instance, it struggled to pick multiples apple at the same time or classify small size apples. Moreover, since the colour of apples is affected by different lighting we had to augment our dataset. 


### Data preprocessing 

### Dataset augmentation. 

To achieve better performance and accuracy we had to augment our data to tackle extreme case. 
By using python code we achieve to ; 
darkening and lightening image
reducing the size of apple while keeping the same background
putting multiples apple on single pictures.

![0000](https://github.com/eliseSou/eliseSou.github.io/assets/104540427/aaa94e67-1716-4aff-837e-971f1fa78c06){: width="100" height="100"}
![148482](https://github.com/eliseSou/eliseSou.github.io/assets/104540427/11cab4df-92ca-4330-a865-fcfa0fa329cd)
![175447](https://github.com/eliseSou/eliseSou.github.io/assets/104540427/88a18cc1-b5fe-4037-ba9d-90aa2d076c86)
![67587](https://github.com/eliseSou/eliseSou.github.io/assets/104540427/84f75e89-a78a-4ec2-ae5e-85a800f01d27)
![94552](https://github.com/eliseSou/eliseSou.github.io/assets/104540427/37482c0c-7479-4333-acbf-9acc8debd1dd)
![121517](https://github.com/eliseSou/eliseSou.github.io/assets/104540427/7c13b17b-ae2e-4302-ac43-d00c23af5770)



System evaluation 
------------------

Precision: 
Recall: 
mAP50: 
mAP50-95: 

Not Augmentation
|Class|Images|Instances|Precision|Recall|mAP50|mAP50-95|
|------|---|---|---|---|---|---|
|All|6740|6740|0.551|0.775|0.642|0.632|
|A|6740|1845|0.496|0.713|0.588|0.581|
|B|6740|3426|0.557|0.948|0.68|0.673|
|C|6740|1469|0.601|0.663|0.658|0.643|

Augmentation (Size, Brightness, Synthesis) & Segmentation

|Class|Images|Instances|Precision|Recall|mAP50|mAP50-95|
|------|---|---|---|---|---|---|
|All|6740|6740|0.323|0.667|0.363|0.357|
|9(C)|6740|154|0.283|0.377|0.297|0.286|
|10(C)|6740|676|0.313|0.641|0.333|0.327|
|11(B)|6740|1371|0.332|0.694|0.371|0.363|
|12(B)|6740|1851|0.318|0.85|0.381|0.377|
|13(A)|6740|1686|0.367|0.797|0.414|0.409|
|14(A)|6740|1002|0.328|0.641|0.382|0.377|

Applicaion demonstration
-------------------


Reflection 
----------------


Broader Impacts
--------------
