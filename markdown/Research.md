## Deep Contrastive Learning for Code Authorship Recognition
 
Code authorship identification can assist in identifying creators of malware, identifying plagiarism, and giving insights into copyright infringement cases. The Commonwealth of Virginia, where I attend college at James Madison University, has a vested interest in this work as it relates to cybersecurity. As such, my lab has received a Commonwealth Cyber Initiative grant to pursue author identification research using deep learning.

### Background

Previous work, in both small and large scale author recognition, focused on using handcrafted features fed into a machine learning system [1]. However, results have consistently shown that letting a deep neural network learn the important features gives better results [2]. Large-scale author recognition has taken advantage of neural networks but rather than training their models directly on the code, these works trained their models on TF-IDF (term frequency-inverse document frequency) vectors [3][4]. TF-IDF vectors contain ratios of term frequencies and document frequencies for each token in a fixed vocabulary. Unfortunately, the TF-IDF vectors discard all formatting information, in contrast to training the model directly on the code. Additionally, the document frequency may have trouble extrapolating to code outside the original dataset distribution, limiting its applicability. Abuhamad et  al. did explore training a model directly on code files, however, they were unable to match or exceed the accuracies of models trained on precomputed TF-IDF vectors using the same model [3].

Contrastive learning works by using a neural network to project a given sample as a vector and then training it to pull similar samples together and push different samples apart [5]. We measure the distance between similar and dissimilar pairs by the cosine distance between their projections which has been empirically shown to provide better results over euclidean distance in a margin loss [5][6]. Additionally, NT-Xent uniformly distributes samples on the surface of the hypersphere they project onto [7]. In my lab’s case, we want to minimize the distance between projections of code written by the same author, and maximize the distance between code written by different authors (Figure 1).
![](https://lh3.googleusercontent.com/-DornR798bW_9W_IJgLmQ56roNjsWNwpvI2lOzfTfxsmu4MKaivSclRX-wvGvpWX_WVPGEJu2DmnHiFvaVM9WXYwrOMori5g8jdktKv4VqbjmCgIfXI21r9bNrfbg4qGTGIbmCTi)![](https://lh3.googleusercontent.com/kIBNdN0UkVj6dPOJKiFmQH_2nicuE1TF39dR3xv6dNbYt7QC7ObHWIp0wxc0Q5GLhIl23jXGHmz4Qb7xJxgd4-9iDMr-_TU_r48edbzM-iG_P8uxgjAoT1KwRKA-G20jMxZYXNE-)

Figure 1. Applying a dimensionality reduction technique (PCA), we can visualize the author projections in 2D. The figure on the right shows the projections of code files of 5 authors from a trained contrastive model. The figure on the left shows the projections of an untrained model. This shows that the contrastive model is separating different authors in the vector space.

### Methods

After my initial efforts did not produce the results I hoped for, I proposed contrastive learning to Dr. Sprague as a solution. Author identification presents itself as a strong application of recent advances in contrastive learning, a technique facial recognition research has already shown can be an effective way to identify a large number of individuals  [8]. I base my implementation on the contrastive loss function, NT-Xent [5]

Having this contrastive projection does not immediately solve the problem and classify the authors. To do the actual prediction, I must train a secondary classifier. Ideally, I want a linearly separable projection so that I can use a simple classifier such as linear regression or k-nearest neighbors to do the prediction. Simple classifiers allow for increased interpretability and are easily repurposed for a new set of authors without having to train a new neural network. The latter gives the flexibility needed from an identification system in the rapidly changing domain of malware.

Recognition tasks fall into two categories: closed set and open set. For closed set recognition, there is a known set of authors and the goal is to assign an unlabeled sample of code to an author in that set. In the open set case, there is no fixed set of authors. Instead, the goal is to determine whether two code samples have the same author. One advantage of our approach is that it lends itself to open set recognition. I can only report results for closed set recognition at this point in time.

To evaluate the effectiveness of my contrastively trained models on unseen authors, I created our train, validation, and test datasets to have disjoint sets of authors. Consistent with the general observation that letting deep neural networks train on raw data improves results, I train a 1D-CNN model directly on the code files using the NT-Xent loss [5][9]. I then applied the model to the code and authors in the validation set and used the resulting projections to perform cross-validation on a secondary classifier. We use code from the Google Code Jam coding competition as our dataset consistent with previous work in this area [1][3][4].

Results![](https://github.com/riels89/riels89.github.io/blob/master/results_table.png?raw=true)
Figure 2. Best accuracies reached by previous work withthe number of authors tested on. All results used files perauthor.
*Our implementation of Abuhamd et al.’s work results inmuch lower accuracies. The only difference in implemen-tation is the word/token encodings because we do not haveaccess to the authors implementation. We use our unigramlanguage model encodings.

My current results do not match the accuracies of previous work (Figure 2); however, given that the authors I evaluated have not been seen by the contrastive model, a drop in accuracy is expected. In contrast, previous work trained and evaluated their entire model on the same set of authors. While the accuracies do not yet compare to previous work, these results do show that the contrastive models generalize well to unseen authors.


### Discussion

Our lab’s method has some advantages over previous work even if we do not end up improving on classification accuracy:

-   Inherit out of distribution detection--Because training a model contrastively results in uniform projections of code and authors, if a code file is analyzed that is not from any author being considered, the model will separate it from the other code files in the vector space. I will be pursuing open-set results to show this empirically.
    
-   Increased interpretability--We can see how similar two authors or pieces of code are. This is desirable in plagiarism cases because you can see how similar each author’s code usually is and if the code in question is an outlier, in contrast to a more opaque classification decision.
    
-   Easily classify new authors--When using a simple secondary classifier such as k-nearest neighbor, classification of new authors is simple. In previous work, new authors would require the, often non-trivial, retraining of the model.
    
-   Easily applied to new languages--Since our approach has no handcrafted features to make, training only requires the source code.
    

### Future Work

Previous work achieved their results by training a model from scratch with one set of authors. In order to get directly comparable results, rather than starting with an untrained model, I will retrain the contrastive model on the validation set. This well-known technique, called transfer learning, can allow models to improve on their supervised baselines [5]. Another way to get directly comparable results is to evaluate authors that the contrastive model has already seen. Caliskan-Islam et al. configured their experiments to prove their model was only capturing style information and not author skill or which problems were being solved (data was from coding competition) [1]. I will construct a similar experiment to compare the results, and to ensure the quality of this work.

This summer, I conducted research into contrastive learning for unsupervised image segmentation on brain microscopies at Howard Hughes Medical Institute’s Janelia Research Campus. This work and my summer experience have complemented each other, allowing me to move much quicker and I believe will ultimately lead to better results. While at James Madison University as an undergraduate, I want to continue working with contrastive learning and hope to explore new applications or theoretical questions in my undergraduate thesis. 

References

[1] A. Caliskan-Islam et al., 24th Usenix Security Symposium, pp. 255–270. 2015.

[2] LeCun, Y., Bengio, Y. & Hinton, G. Nature  521, 436–444 2015.

[3] M. Abuhamad et al., Future Generation Computer Systems. 95, 104–115. 2019.

[4] M. Abuhamad, T. AbuHmed, A. Mohaisen, D. Nyang, Computer and Communications Security (CCS), pp. 101–114. 2018.

[5] T. Chen, S. Kornblith, M. Norouzi, G. Hinton, Int. Conference on Machine Learning (ICML). 2020.

[6] Raia Hadsell, Sumit Chopra, Yann LeCun, Conference on Vision and Pattern Recognition (CVPR). workshops. 2006.

[7] T. Wang, P. Isola, Int. Conference on Machine Learning (ICML).  2020.

[8] I. Masi, Y. Wu, T. Hassner, P. Natarajan, 31st SIBGRAPI, pp. 471–478. 2018.

[9] A. Conneau, H. Schwenk, L. Barrault, Y. Lecun, European Chapter of the Association for Computational Linguistics EACL, 1107–1116 . 2017.

## Contrastive Learning for image segmentation
### Howard Hughes’ Medical Institute's Janelia Research Campus, Undergraduate Scholar    Summer 2020
*Researched applying unsupervised deep contrastive learning to image segmentation, with a focus on neuron and cell segmentation from microscopies, under Dr. Jan Funke in Janelia’s Funke Lab.*

Segmenting each neuron of a drosophila brain by hand from electron microscopy data would take decades. Were this task to be successfully automated, it would allow for a much better understanding not only of neural circuitry but any biological research needing segmentation. Deep learning has been the centerpiece of automatic segmentation; however, these approaches need exorbitant amounts of labeled data which is expensive and time-consuming to collect. I collaborated with Dr. Funke to formulate image segmentation as an unsupervised contrastive learning problem to take advantage of the vast amount of unlabeled data that already exists.

I built the preprocessing and training pipeline for my model to work with both 2D/3D data and handle the complicated grid search of hyperparameters over the contrastive pre-training and subsequent segmentation tasks. The contrastive models I created were more accurate than the randomly initialized baselines when both were trained on the segmentation task.

## Deepletters: A CNN-LSTM Approach to ASL Fingerseplling Translation 
##### [Github Respository](https://github.com/riels89/DeepLetters)
##### The full [poster](https://riels89.github.io/FinalDraftIntelPoster.pdf)
#
The goal of this work is to produce a AI to translate fingerspelled words from video using a CNN-LSTM. To do this me and my partner will train the model in two steps:
1. Train the CNN on abot 70 thousand static hand images of different letters. The letters J and Z will be excluded because they requrie movement. We are retraining the [Deep Hand](https://www-i6.informatik.rwth-aachen.de/publications/download/1000/KollerOscarNeyHermannBowdenRichard--DeepHHowtoTrainaCNNon1MillionHImagesWhenYourDataIsContinuousWeaklyLabelled--2016.pdf) model which was retrained on Google's ILSVRC 2014 Inception net. 
2. Train the LSTM on the last pool layer output from our CNN of our dataset of videos of people signing individual words.

The static CNN base model reached a 90% accuracy on the validation set and 47% on the real-world test set. Another CNN was trained with garbage frames so that the model can tell between a letter or a transition frame. This model reached a 93% validation accuracy, and a 45.5% accuracy on the test set. 

## Effects of the Postal Banking Act 
#### Indroduced by Kirsten Gillibrand, it would alow post offices to perform many basic banking cabablilities including check cashing, small dollar loans, small saving and checking accounts, debt cards, atms, and any other services deemed neccesary. 

My analysis won 1st place at a JMU GIS competition, and was nominated for the national ESRI User Conference Student GIS Competition. 

The project focused specifically on how this bill would effect banking deserts and predetory payday loan lending. The effective area of a financial institution (in this case banks and payday loan lenders) was defined as a 10-mile radius around the location by the New York Fed (Morgan, Donald, et al.) which was used to o analyze the impact of this bill. Post offices were found to cover 98% - 99% of payday loan lenders effective area as well as being in a position to eliminate around 70% - 90% of banking deserts in the three states looked at (California, Texas, and Alabama).

Scroll through or go [here](https://arcg.is/0C5m5i) to see it in full size.

<iframe width="100%" height="800px" src="https://sbhs-gis.maps.arcgis.com/apps/Cascade/index.html?appid=c77d0b8ff7b440dcbda6cb6c502f75f0" frameborder="0" scrolling="yes"></iframe>
