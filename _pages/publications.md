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

After brainstorming together we came up with a few ideas: text summarizer for college students, product recommendation for a shopping site. But eventually, we choose to develop a model which could predict the sweetness of apples based on pictures. We wanted to create a project which could be useful in everyday life with direct application. 
As of today, to predict the sweetness of fruit there is one solution: the refractometer. A refractometer is a small tool, on which you are supposed to put a few drops of the product you want to measure and then you will see the sugar level in terms of percentage. In reality, this tool measures the refraction of the juice, which is influenced by the level of sugar. This method is the most accurate way, but it requires breaking the fruit every time, thus making it unusable while grocery shopping. 

Indeed, our goal was to create a simple application which you could use on your phone to choose the best fruit possible.  Moreover, the colour of a fruit is correlated to its sugar level, which is why we believe that is possible to predict a fruit’s sweetness based on a simple photo. However machine learning is as powerful as the dataset let it be, so we were limited by available datasets, hence why we choose to develop this project for apples only. You can find the original dataset [here](https://www.aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100&aihubDataSe=realm&dataSetSn=490).




System Design
-------------

To make our project work we needed machine learning model which could detect apples and predict their sweetness, a server to host the trained model and the dataset, and a client-side application which could take pictures as input and communicate with the server. 


### Web Application

The flow starts with the user, who interacts with the system by making a request or accessing a service. The request then travels over the internet, where it reaches the Internet Gateway. The Internet Gateway acts as the entry point, connecting the internet to the AWS Cloud infrastructure.

Within the AWS Cloud, the primary networking component is the Virtual Private Cloud (VPC). It allows you to create an isolated virtual network in the cloud and define subnets, security rules, and routing configurations.

The VPC consists of several components, including the Public Subnet. A Public Subnet is a subdivision of the VPC that is configured to be accessible from the internet. It has an associated route table that directs traffic in and out of the subnet.

To control the traffic flow and security, a Security Group is employed. A Security Group acts as a virtual firewall that defines inbound and outbound rules for network traffic to and from the associated resources. It ensures that only allowed traffic can reach the resources and protects them from unauthorized access.

Finally, the EC2 Instance resides within the Public Subnet. An EC2 Instance is a virtual server running in the cloud that can be used to host applications, websites, or perform various computing tasks. It is a fundamental building block in AWS and serves as the endpoint for the user's request after passing through the internet, Internet Gateway, VPC, and Public Subnet.


<img width="834" alt="image" src="https://github.com/eliseSou/eliseSou.github.io/assets/127825259/39ae181f-8388-402f-9258-d2675815b704">


### Mobile phone application 

We changed the .pt format model trained on the server to .mlmodel format and then apply the image from the smartphone to the model using the UI to detect the apple and classify the sugar sweetness.

<img width="640" alt="스크린샷 2023-06-07 오후 4 40 48" src="https://github.com/eliseSou/eliseSou.github.io/assets/125421860/6c965beb-2397-46e1-b6a3-4683a0d0a1d6">

Machine Learning component 
----------------

To achieve our goal we needed a model capable to detect many apples in a frame, and then applying regression based on the detected apples to predict their sweetness level.


### YOLO model 

For the backbone model, we chose to use a pre-trained YOLO model. We choose this model because it can do at the same time object segmentation and object classification. 
After a few trials with different versions, we concluded that YOLOv5 was the most efficient for our project. 

Then we trained it with the appel dataset and evaluated it through our laptop webcam with pictures from the dataset and real apples. We noticed some problems in different cases, for instance, it struggled to pick multiples apple at the same time or classify small size apples. Moreover, since the colour of apples is affected by different lighting we had to augment our dataset. 


### Data preprocessing 
The total number of apple data in the AI hub is 535,691. The table below shows the components of the data. 

|Apple Varieties|Data Num|
|------|---|
|Shinano Gold|43,374|
|Arisu|42,130|
|Hongro|190,762|
|Fuji|259,425|
|Total|535,691|

We used 33,707 arisu data for learning and evaluation because of the learning time and storage capacity. (Train: 26,967 (80%), Evaluation: 6740 (20%), Total: 33,707) In addition, because the YOLO model uses 640X480 size images, we resized all images to 640X480
### Dataset augmentation. 

To achieve better performance and accuracy we had to augment our data to tackle extreme case. 
By using python code we achieve to ; 
darkening and lightening image
reducing the size of apple while keeping the same background
putting multiples apple on single pictures.





System evaluation 
------------------

When apples were divided into three classes, mAP50 was 64.2%. At this time, the number of B classes was 3,426, which was much higher than the number of A and C classes, so the mAP50 of B classes was higher than that of A and C.

However, when apples were divided into six classes, mAP50 decreased to 50%. The performance decreased because of the increasing number of classes, but all classes showed similar performance.

No Augmentation

|Class|Images|Instances|Precision|Recall|mAP50|mAP50-95|
|------|---|---|---|---|---|---|
|All|6740|6740|0.551|0.775|0.642|0.632|
|A|6740|1845|0.496|0.713|0.588|0.581|
|B|6740|3426|0.557|0.948|0.68|0.673|
|C|6740|1469|0.601|0.663|0.658|0.643|

Augmentation (Size, Brightness, Synthesis) & Segmentation

|Class|Images|Instances|Precision|Recall|mAP50|mAP50-95|
|------|---|---|---|---|---|---|
|All|6740|6740|0.432|0.621|0.506|0.496|
|9(C)|6740|154|0.492|0.468|0.508|0.491|
|10(C)|6740|676|0.451|0.549|0.512|0.501|
|11(B)|6740|1371|0.422|0.64|0.502|0.49|
|12(B)|6740|1851|0.381|0.726|0.499|0.492|
|13(A)|6740|1686|0.419|0.73|0.506|0.5|
|14(A)|6740|1002|0.425|0.631|0.512|0.504|

Application demonstration
-------------------

IOS Application

Since it is difficult for consumers who want to buy apples at the supermarket or market to select high-sugar apples by measuring the sugar content by themselves, we developed an easily accessible application (only for IOS) to help them select high-sugar apples.
The app. has two modes: 'Live Classification', which shows the sugar content of apples in real time through the phone's camera, and 'Photo Classification', which shows the sugar content of apples in the photo.
The color of the bounding box is different depending on the sugar classes of the apples, and the quantity per class is shown in the table to better understand the number per class when there are many apples.

<img width="800" alt="스크린샷 2023-06-07 오후 4 25 06" src="https://github.com/eliseSou/eliseSou.github.io/assets/125421860/ff7b7f07-d86e-4c46-b566-65814c246283">

(a) is the main page of the app, (b) is the page that detects apples and classifies sugar sweetness in real time, (c) shows the result of the moment when you press the capture button in (b), and (d) shows the number corresponding to the sugar sweetness when you press the table icon in (c).


**Web Application**

The main utility of our app is to enable users to non-destructively measure the sweetness of an apple in real-time. To achieve real-time functionality, we have decided to build a web application utilizing a webcam. Our application is well-suited for locations such as farms and markets, where apple sweetness measurement and classification can be performed, allowing for informed selection.

![Capture](https://github.com/eliseSou/eliseSou.github.io/assets/127825259/f91157ac-5520-4e9d-91cb-1b9497fa1bf1)

To use the web application:
1. After preparing the apples, Go to http://15.165.32.149:8501/Webcam_with_YOLOv5_apple.
2. Click on “start button” to start the webcam.


Reflection 
----------------
**Challenges and how we overcome them:**
1. Data augmentation:

The sweetness of the apple is influenced by the color and shape of the apple, and the color of the apple depends on the light. Therefore, when measuring the sweetness of the apple with a webcam, there was a big change in the prediction depending on the amount of light the apple receives.

In addition, the apple dataset that exists in the AI Hub has only one apple in one image, and in the dataset, there is no small size apple. Therefore, there have been cases where several small-sized apples are not well detected.

To solve this problem, data augmentation was conducted. First, to reduce the effect of light, brighter, darker apples were added to the existing data, and we made synthesized images that contain several sizes of apples in a single image, and made images that have small size apple.

2. Server design:

We encountered issues when attempting to deploy the app easily through Streamlit Community Cloud to a remote server. To establish a media stream connection, it was necessary to configure STUN/TURN servers. While free STUN servers provided by Google were available, media streaming did not function properly in our network environment. Through this document (https://github.com/whitphx/streamlit-webrtc), we learned that WebRTC packets could be blocked when the client is behind a firewall. As a result, we made the decision to build and deploy our own server directly through AWS.

3. changing our buisness plan: 

Initially, we aimed to develop a model for small farms, assisting farmers in classifying and selling their products based on fruit sweetness. We required a model capable of swiftly detecting and classifying apples on a conveyor belt. However, we discovered that our model was too slow and struggled to identify multiple apples in the same image.

Consequently, we quickly devised an alternative solution by redirecting our product towards a different target audience. We successfully implemented our model into a mobile phone application, catering to personal use. Simultaneously, we continue to work on developing a model suitable for industrial use and plan to deploy it on a web server.

4. Communication 

At first, it was tough communicating together as our team is composed of three Korean students and one international student. Different languages and cultures made it challenging to understand each other. But we didn't let that stop us! We found ways to improve, like using translation tools and having weekly team meetings. As we worked together and listened to each other, our communication skills got better, and we became a stronger team. 



**Future work:**

1. Generalizability to other fruits:

The approach of using a deep learning model to evaluate fruit quality can be extended to other fruits besides apples. This can enable the detection of the growth, quality, or sweetness of different fruits, thereby having a broader impact on the agricultural industry.

2. Small size apple detection

Even though data augmentation was performed, the small size apple was not well detected. If we change the data augmentation method or add more data, the small size apple will be detected.

3. Use more apple varietites

We only used Arisu data in this project. However, apples will be different in color and shape depending on the variety. Therefore, it will be very difficult to predict the sweetness of other varieties of apples. In the future, apple varieties such as Hongro or Fuji will also be used for learning.


Broader Impacts
--------------

We achieved our goal of finding the sweetness of apples based on pictures, and we believe our work could be useful in the industry. Indeed, sorting and grading apples ensure that the consumer receives high-quality products and more to their liking. Customers could choose between a more intense taste or a milder taste. This could lead to an increase in the consumption of fruit which would have a positive impact on people’s health.

In addition, our app can contribute to market transparency. Because our app can provide objective measurements of apple sweetness. This can empower consumers to make informed decisions and can promote fair competition among apple farmers.
