## [CS231n](http://cs231n.stanford.edu/) (Fall 2017 - present) 
#### [Github Repository](https://github.com/riels89/CS231n)

To be clear I am not offcially taking this class nor am I a student of Stanford. I am using the lectures and assignments which are provided  online for Free. 

I am using the Spring 2017 version (future iterations of the class will be diffrent)

In this class you make and implement:

* K nearest neighbor
* Linear SVM
* Softmax Classifier
* Two-layer neural network
* N-layer neural network with diffrent update models, batch normalization, and dropout
* Convolutional Neural Nework
* Neural Network using Tensorflow
* RNN using Tensorflow
* LSTM with Tensorflow
* Style transfer network using Tensorflow
* GAN using Tensorflow

My finial project for the class will be

## Twitter Sentiment Map (Fall 2017)
#### [Github Repository](https://github.com/riels89/-Twitter-Sentiment-Map)

<style>.embed-container {position: relative; padding-bottom: 80%; height: 0; max-width: 100%;} .embed-container iframe, .embed-container object, .embed-container iframe{position: absolute; top: 0; left: 0; width: 100%; height: 100%;} small{position: absolute; z-index: 40; bottom: 0; margin-bottom: -15px;}</style><div class="embed-container"><small><a href="//sbhs-gis.maps.arcgis.com/apps/Embed/index.html?webmap=1f671c7b5bce4fceb743340521e5b62f&amp;extent=-137.4089,11.4506,-29.4792,57.5233&zoom=true&scale=true&legend=true&disable_scroll=false&theme=dark" style="color:#0000FF;text-align:left" target="_blank">View larger map</a></small><br><iframe width="500" height="400" frameborder="0" scrolling="no" marginheight="0" marginwidth="0" title="Twitter Sentiment Map - Trump (embedding version)" src="//sbhs-gis.maps.arcgis.com/apps/Embed/index.html?webmap=1f671c7b5bce4fceb743340521e5b62f&amp;extent=-137.4089,11.4506,-29.4792,57.5233&zoom=true&previewImage=false&scale=true&legend=true&disable_scroll=false&theme=dark"></iframe></div>

This map is showing the average twitter sentiment of Donald Trump across each state. I gathered tweets from twitter (about 125,000) that had the key word "Trump", and preformed sentiment anaylsis on them using a voting classifier consisting of a standard Naive Bayes, NuSVC, LinearSVC, SGDC, multinomialNB, BernoulliNB, and LogisticRegression. The classifier would rate it postive (1) or negetive (-1). The tweets were stored in a MySQL database along with their location,  and twitter id. Location was based of what each person put as thier state in the location field in their profile. Anyone who didn't have a vaild location in a US state was discarded. I also put a cap of 3,000 tweets from each state to avoid having 60% of my data from only Texas and California. In the future I would like to try using an LSTM to do the sentiment analysis, because they preform very well on sequences of data. I used ArcGIS to display the data.

[Here](https://arcg.is/1znnDD) is my full analysis of the data. 

## Java Neural Network on Iris Flower Dataset (Spring 2017)
#### [Github Repository](https://github.com/riels89/IrisFlowerJavaNN)

This was my first attempt at a machine learning project so I used a basic data set. The Iris flower dataset has sepal and pedal width and length that belonged to 3 diffrent types of flowers. The neural network I trained had 2 layers and acheived about a 95% accuracy on average on the test data set. 
![NN](https://i.gyazo.com/f918bc03aed8c89d37f326b386f78d8f.png)

(The size of the weights indicates its strength!)

Here is the code snipet that gives you the basic idea of how I structured the NN.
```Java
public void trainOne()
	{
		currentInput = trainingData[dataIndex];
		forwardPropagate();
		backPropagate();
		
		last200.add(wasRight(trainingAnswers[dataIndex]));
		if (last200.size() > 200)
			last200.remove(0);
		
		dataIndex++;
		if(dataIndex>=trainingData.length)
			dataIndex=0;
	}
 ```
 
 Looking back on the code with what I know today I can easily spot mistakes. For example using a sigmoid function on the output neuron:
 ```Java
 public double activate(double[] inputs)
	{
		netInput = dot(inputs, weights);
		switch(AF)
		{
			case  SIGMOID:
				output = sigmoid(netInput);
				break;
			case ReLU:
				output = Math.max(0, netInput);
				break;
		}
		deltaOutput = output * (1-output);
		return output;
	}
  ```
... Never use a sigmoid.

## Graphing Servlet (Winter 2017)
#### [Github Repository](https://github.com/riels89/GraphingServlet)

I created a Java servlet using Apache Tomcat that displays images of graphs that it created. The actual graphing part isn't very good and only exists so that I could put stuff in a database. It creates a graph and stores the points in a MySQL database. Another part of the program pulls the points and creates the image of the graph. It stores the image in the file stystem and the file path in the database. The servlet then pulls the file paths from the database, finds the files, then displays the images. 

