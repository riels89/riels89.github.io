
## Twitter Sentiment Map (Fall 2017)
##### [Github Repository](https://github.com/riels89/-Twitter-Sentiment-Map)

<style>.embed-container {position: relative; padding-bottom: 80%; height: 0; max-width: 100%;} .embed-container iframe, .embed-container object, .embed-container iframe{position: absolute; top: 0; left: 0; width: 100%; height: 100%;} small{position: absolute; z-index: 40; bottom: 0; margin-bottom: -15px;}</style><div class="embed-container"><small><a href="//sbhs-gis.maps.arcgis.com/apps/Embed/index.html?webmap=1f671c7b5bce4fceb743340521e5b62f&amp;extent=-137.4089,11.4506,-29.4792,57.5233&zoom=true&scale=true&legend=true&disable_scroll=false&theme=dark" style="color:#0000FF;text-align:left" target="_blank">View larger map</a></small><br><iframe width="500" height="400" frameborder="0" scrolling="no" marginheight="0" marginwidth="0" title="Twitter Sentiment Map - Trump (embedding version)" src="//sbhs-gis.maps.arcgis.com/apps/Embed/index.html?webmap=1f671c7b5bce4fceb743340521e5b62f&amp;extent=-137.4089,11.4506,-29.4792,57.5233&zoom=true&previewImage=false&scale=true&legend=true&disable_scroll=false&theme=dark"></iframe></div>


This map is showing the average twitter sentiment of Donald Trump across each state. I gathered tweets from twitter (about 125,000) that had the key word "Trump", and preformed sentiment anaylsis on them using a voting classifier consisting of a standard Naive Bayes, NuSVC, LinearSVC, SGDC, multinomialNB, BernoulliNB, and LogisticRegression. The classifier would rate it postive (1) or negetive (-1). The tweets were stored in a MySQL database along with their location,  and twitter id. Location was based of what each person put as thier state in the location field in their profile. Anyone who didn't have a vaild location in a US state was discarded. I also put a cap of 3,000 tweets from each state to avoid having 60% of my data from only Texas and California. In the future I would like to try using an LSTM to do the sentiment analysis, because they preform very well on sequences of data. I used ArcGIS to display the data.

[Here](https://arcg.is/1znnDD) is my full analysis of the data. 



## Convolutional Neural Networks for Visual Recognition (Fall 2017-Spring 2018)
##### [Github Repository](https://github.com/riels89/CS231n)
Went through this Stanford class on own time which is focused on deep learning and computer vision.  The class is using Python to achieve a deep understanding of how to create major algorithms like CNNs and LSTMs by hand. From there the same algorithms are implemented in Tensorflow. This class was very helpful to understanding all of the algorithms at a deeper level.

Algorithms implemented:
* K-nearest neighbor
* SVM
* Softmax classifier
* Two layer Neural Network
* Batch Normalization
* Dropout
* CNN
* Vanilla RNN
* LSTM
* Saliency Maps
* Style Transfer

Coursework was done from the materials put online and without official enrollment of the course.

## Neural Network on Iris Flower Dataset (Spring 2017)
##### [Github Repository](https://github.com/riels89/IrisFlowerJavaNN)

Created a simple two-layer neural network from scratch in java for my AP computer science class' final project. Used the infamous Iris dataset containing data of sepal and pedal width and length belonging to 3 types of flowers. 

## Graphing Servlet (Fall 2016)
##### [Github Repository](https://github.com/riels89/GraphingServlet)

This graphing servlet is not very good at graphing and will break if you attempt to put in complicated functions.
It was mostly made to show the creation of a servlet, the use of a database, and to use images in a servlet with Java.
