---
layout: archive
title: "Publications"
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
+ Liu hyongsig
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

### Hosting server

The goal of this server was to host all the dataset and then train the model with GIST's CPU. 

### Streamlit and Webserver

At first we wanted to create a web application, 

### Mobile phone application 


Machine Learning component 
----------------

### YOLO model 

### Data augmentation


System evaluation 
------------------


Applicaion demonstration
-------------------


Reflection 
----------------


Broader Impacts
--------------
