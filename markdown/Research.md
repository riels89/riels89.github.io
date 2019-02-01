## Deepletters: A CNN-LSTM Approach to ASL Fingerseplling Translation 
### (Paper still in progress) 
##### [Github Respository](https://github.com/riels89/DeepLetters)
#
The goal of this paper is to produce a AI to translate fingerspelled words from video using a CNN-LSTM. To do this me and my partner will train the model in two steps:
1. Train the CNN on abot 70 thousand static hand images of different letters. The letters J and Z will be excluded because they requrie movement. We are retraining the [Deep Hand](https://www-i6.informatik.rwth-aachen.de/publications/download/1000/KollerOscarNeyHermannBowdenRichard--DeepHHowtoTrainaCNNon1MillionHImagesWhenYourDataIsContinuousWeaklyLabelled--2016.pdf) model which was retrained on Google's ILSVRC 2014 Inception net. 
2. Train the LSTM on the last pool layer output from our CNN of our dataset of videos of people signing individual words.

We also have collected some original data from ASL classes at our school by taking videos of them signing. Our other sources of video data are parsed videos taken from the internet. 

## Effects of the Postal Banking Act 
#### Indroduced by Kirsten Gillibrand, it would alow post offices to perform many basic banking cabablilities including check cashing, small dollar loans, small saving and checking accounts, debt cards, atms, and any other services deemed neccesary. 

My analysis won 1st place at a JMU GIS competition, and was nominated for the national ESRI User Conference Student GIS Competition. 

The project focused specifically on how this bill would effect banking deserts and predetory payday loan lending. The effective area of a financial institution (in this case banks and payday loan lenders) was defined as a 10-mile radius around the location by the New York Fed (Morgan, Donald, et al.) which was used to o analyze the impact of this bill. Post offices were found to cover 98% - 99% of payday loan lenders effective area as well as being in a position to eliminate around 70% - 90% of banking deserts in the three states looked at (California, Texas, and Alabama).

Scroll through or go [here](https://arcg.is/0C5m5i) to see it in full size.

<iframe width="100%" height="800px" src="https://sbhs-gis.maps.arcgis.com/apps/Cascade/index.html?appid=c77d0b8ff7b440dcbda6cb6c502f75f0" frameborder="0" scrolling="yes"></iframe>
 


## Twitter Sentiment Map (Fall 2017)
##### [Github Repository](https://github.com/riels89/-Twitter-Sentiment-Map)

<style>.embed-container {position: relative; padding-bottom: 80%; height: 0; max-width: 100%;} .embed-container iframe, .embed-container object, .embed-container iframe{position: absolute; top: 0; left: 0; width: 100%; height: 100%;} small{position: absolute; z-index: 40; bottom: 0; margin-bottom: -15px;}</style><div class="embed-container"><small><a href="//sbhs-gis.maps.arcgis.com/apps/Embed/index.html?webmap=1f671c7b5bce4fceb743340521e5b62f&amp;extent=-137.4089,11.4506,-29.4792,57.5233&zoom=true&scale=true&legend=true&disable_scroll=false&theme=dark" style="color:#0000FF;text-align:left" target="_blank">View larger map</a></small><br><iframe width="500" height="400" frameborder="0" scrolling="no" marginheight="0" marginwidth="0" title="Twitter Sentiment Map - Trump (embedding version)" src="//sbhs-gis.maps.arcgis.com/apps/Embed/index.html?webmap=1f671c7b5bce4fceb743340521e5b62f&amp;extent=-137.4089,11.4506,-29.4792,57.5233&zoom=true&previewImage=false&scale=true&legend=true&disable_scroll=false&theme=dark"></iframe></div>


This map is showing the average twitter sentiment of Donald Trump across each state. I gathered tweets from twitter (about 125,000) that had the key word "Trump", and preformed sentiment anaylsis on them using a voting classifier consisting of a standard Naive Bayes, NuSVC, LinearSVC, SGDC, multinomialNB, BernoulliNB, and LogisticRegression. The classifier would rate it postive (1) or negetive (-1). The tweets were stored in a MySQL database along with their location,  and twitter id. Location was based of what each person put as thier state in the location field in their profile. Anyone who didn't have a vaild location in a US state was discarded. I also put a cap of 3,000 tweets from each state to avoid having 60% of my data from only Texas and California. In the future I would like to try using an LSTM to do the sentiment analysis, because they preform very well on sequences of data. I used ArcGIS to display the data.

[Here](https://arcg.is/1znnDD) is my full analysis of the data. 
