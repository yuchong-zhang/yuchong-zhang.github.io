---
title: "Hoop or ball? customized object detection"
collection: projects
permalink: /projects/object_detection
excerpt: 'A python project to detect hoops and balls in pictures'
projecturl: 'https://github.com/yuchong-zhang/object-detection-hoop_and_ball'
tags:
  - Python
  - DL
---

<a href='https://github.com/yuchong-zhang/object-detection-hoop_and_ball'>See repo here</a>

In this project I use the <a href='https://github.com/tensorflow/models/tree/master/research/object_detectiontensorflow'>object detection API</a> to build a model to detect hoop and ball from pictures. I give lots of credit to <a href='https://pythonprogramming.net/introduction-use-tensorflow-object-detection-api-tutorial/'>this tutorial</a>, which gives step-by-step instructions to build a model to detect mac-n-cheese. In my case, I only used 9 images for training and 4 images for testing while still getting some reasonable results (such as the following image). One can easily get a more accurate model by training with more samples.

<img class="alignnone  wp-image-577" alt="drsg" src="https://yuchong-zhang.github.io/images/object_detection.png" width="1291" height="743"/>
