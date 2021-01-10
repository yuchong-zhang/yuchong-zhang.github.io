---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

Education
------
* Ph.D. in Chemical Engineering, Rice University, 2019
* M.S in Statistics, Rice University, 2020
* M.S in Computer Scinece, Georgia Institute of Technology, 2022 (expected)
* B.S. in Polymer Materials & Engineering, Zhejiang University, 2014

Work experience
------
* 2019 – Present: Data Scientist, Schlumberger
  * Apply deep learning and other machine learning methods to predict the health status of assets using sensor data, classify different failure modes and generate risk index for the whole fleet.

* 2015 – 2019: Doctoral Research Assistant, Rice University
  * Rice University
  * Develop theories and algorithms to model thermodynamics of branched molecular systems.
  * Supervisor: Prof. Walter Chapman

* 2012 – 2014: Graduate Teaching Assistant, Rice University
  * Undertake four terms of graduate teaching assistant work.
  
Skills
------
* Statistical/Machine/Deep learning
  * LR, KNN, SVM, RF, PCA, k-means
  * LSTM, CNN
* Programming
  * Python (numpy, pandas, scikit-learn, keras, matplotlib, bokeh, flask, pyspark...)
  * SQL, bash, R, Matlab, Fortran, C
* Project/Product development
  * Cloud platfrom, git, docker, dataiku 
* Statistics/Maths
  * Bayesian, Mente Carlo, experiment design
  * Fourier transform, density functional theory 
* Domain knowledge
  * Prognostics Health Management (PHM), thermodynamics, polymers

Publications
------
  <ul>{% for post in site.publications reversed%}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>
  
Talks
------
  <ul>{% for post in site.talks reversed%}
    {% include archive-single-talk-cv.html %}
  {% endfor %}</ul>
  

