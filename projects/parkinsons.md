---
layout: page
title: WomenTechWomenYes
---


### What is Parkinsons?

Parkinson's is a very harsh incurable disease, in medical terms it is disorder of the central nervous system. So, people who have Parkinson's gradually loses the ability to control their body movements. Surprisingly, 10,000,000 people suffering from Parkinsons around the world !

### Project Goal

To bulid a model that can detect Parkinson’s disease based on hand-drawings. Hopefully, this model wil be used to detect Parkinson's in early stages.

### Work Stages

#### Data acquisition

At the beginning, their was lack of data problem where I overcame that by Data Augmentation using Image Generator where I increased number of images till I got 7.2K as a training data set size and 2k as testing data size.


###### Data Sample
* Healthy
![healthy]({{ site.url }}/images/healthy.png)
* Parkinson's
![parkinsons]({{ site.url }}/images/parkinsons.png)

#### Baseline Model

Regarding baselining I tried both simple and complex models and neither one of them worked.
Convolutional Neural Network: 40% accuracy 
Random Forest: 60% accuracy 

#### Data Preprocessing

In this step I tried multiple techniques to find the best technique that performs the best on my data. At first I tried to convert image colors to black and white and it didn't work. After that I tried to do edge detection an the model didn't perform well too. So, what I found that if I blur out the noise out of the image and sharpen the spiral my model performs the best.
![parkinsons]({{ site.url }}/images/parkinsons_preprocessing.png)

#### Final Model

After a lot of trails to find the best hyperparameters and number of layers for my Convolutional Neural Network model I got 91% as a validation accuracy. 

##### Result 
I found that CNN performs good enough:
![parkinsons]({{ site.url }}/images/parkinsons_cm.png)

So After that I tried to test the model my self I draw a spiral and I passed it to the model and Alhamdullilah I'm healthy!
![parkinsons]({{ site.url }}/images/healthy_test.png)

And then I tried to draw a spiral mimicking the Parkinson's patients pattern: 

![parkinsons]({{ site.url }}/images/parkinsons_test.png)



### Conclusion and Future work

To conclude I hope that the model would be used for Parkinson's early stage diagnoses. and for future work:
* Gather more data about Parkinson’s patients to improve the model performance.
* Build a Flask app to enhance the model usability.


Have questions or suggestions? Feel free to [email me](mailto:njoud.algifari@gmail.com).

Thanks for reading!
