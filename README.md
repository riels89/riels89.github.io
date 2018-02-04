## [CS231n](http://cs231n.stanford.edu/) (Fall 2017 - present) 


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

##Twitter Sentiment Map (Fall 2017)


<style>.embed-container {position: relative; padding-bottom: 80%; height: 0; max-width: 100%;} .embed-container iframe, .embed-container object, .embed-container iframe{position: absolute; top: 0; left: 0; width: 100%; height: 100%;} small{position: absolute; z-index: 40; bottom: 0; margin-bottom: -15px;}</style><div class="embed-container"><small><a href="//sbhs-gis.maps.arcgis.com/apps/Embed/index.html?webmap=2097a8edb23b4c8ba0e633688d6fde85&amp;extent=-105.5212,20.9162,-62.4548,49.0349&zoom=true&scale=true&legend=true&disable_scroll=true&theme=dark" style="color:#0000FF;text-align:left" target="_blank">View larger map</a></small><br><iframe width="500" height="400" frameborder="0" scrolling="no" marginheight="0" marginwidth="0" title="Twitter Sentiment Map of Trump" src="//sbhs-gis.maps.arcgis.com/apps/Embed/index.html?webmap=2097a8edb23b4c8ba0e633688d6fde85&amp;extent=-105.5212,20.9162,-62.4548,49.0349&zoom=true&previewImage=false&scale=true&legend=true&disable_scroll=true&theme=dark"></iframe></div>


## Java Neural Network on Iris Flower Dataset (Spring 2017)

This was my first attempt at a machine learning project so I used a basic data set. The Iris flower dataset has sepal and pedal width and length the belong to 3 diffrent types of flowers. The neural network I trained had 2 layers and acheived about a 95% accuracy on average on the test data set. 
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
