# Repo Navigation
- First file is git ignore where we ignore jpg images for image classification data. **This is important because file size is too large**
- [Hello_Fresh.ipynb](Hello_Fresh.ipynb) Beef image classification notebook
- [Presentation](Hello_Fresh_Presentation.pdf)
- [Hello_Fresh_Review_Analysis.ipynb](Hello_Fresh_Review_Analysis.ipynb) NLP review text classification notebook
- Other files can be ignored

# Hello-Fresh
## Business Understanding
- StakeHolder - **HelloFresh**
- Society as a whole has been trending to delivery services so it saves "you" the consumer time and lessens human interaction.
    - We see this in many facets of life i.e (Car Services, online food ordering services and, reservation services) .
- HelloFresh takes a different approach than online food delivery like Fresh Direct.
    - Hello Fresh lets you pick a food plan and then they send you a kit with all ingredients weighed out and portioned for you to make.
- Now that the business has reached a mass-produced scale it is important to streamline the process while still having quality food at the same time.
- This is where image classification can play a key role in whether or not identifying beef is fresh or rotten.
- The vision of where to implement this classifier is in cameras that take pictures of meat as they are flowing down the conveyer belt.
    - The camera will snap a picture that then is run through my model and classified as fresh or rotten.
- This classifier can save money as you wont have to use wharehouse workers to check the beef quality and uphold the reputation as the top online food service.
- **reputation is captured in consumer reviews.**
- It is important to capture the sentiment of your customers for a couple of reasons.
1. To build a great reputation and track record that you are a good company that others should be using.
2. That you use customers' negative feedback to look into potential problems and see if there is any truth to that feedback.
- Most of the time this feedback is given in a standard review format with a certain amount of stars and the review text.
- **However, there are times when a customer will just give feedback with no number of stars. You can be losing valuable reviews!!** 
- **There are also times when feedback is not given in the standard way. It can be given through a support call or email.** 
    - **It is important to also capture the sentiment of the text transcripts of these calls and the emails.**
- HelloFresh can use a sentimental analysis from a natural language processing model to capture these missed sentiments to help cast a wider net on reviews which can overall help company performance and brand reputation.
## Data Understanding 
- The **image classification data** comes from [Mendley Data](https://data.mendeley.com/datasets/nhs6mjg6yy/1).
- It has about 3000 images of raw beef; some being fresh and some being rotten.
- Some potential limitations are the amount of data I have; it could be more accurate with more training data.
- The **text classification data** I accumulated comes from [Trustpilot](https://www.trustpilot.com/review/hellofresh.com). Trustpilot is an online review community that connects businesses and consumers through genuine feedback from customers about their buying and service experiences. 
- The raw data from Trustpilot is important because to be able to run a sentimental analysis, you need a good amount of reviews of text and a target.
- There are over 40,000 reviews which give me more than plenty of data to make a NLP model.
- Aside from the text, I used topic modeling to make the data more robust and try and find deeper underlying reasons.
## Beef Image Classification
### EDA
- Example of rotten image
  
![image](https://github.com/ddcots24/Hello-Fresh/assets/131708046/ed294224-1cc3-40a0-813d-ded6e733722a)

- Distribution of rgb values for a rotten image - skewed left
  
![image](https://github.com/ddcots24/Hello-Fresh/assets/131708046/c02543f1-c453-481a-8b72-b0cb2dcf38e0)

- Example of fresh image
  
![image](https://github.com/ddcots24/Hello-Fresh/assets/131708046/83e815d1-da62-4ced-8fff-d233c89c106e)

- Distribution of rgb values for a fresh image - more normally distributed
  
![image](https://github.com/ddcots24/Hello-Fresh/assets/131708046/c9ad5d33-340c-4854-b204-21b26dcf17cc)

### Modeling (Convolutional Neural Network)
- Model training loss

![image](https://github.com/ddcots24/Hello-Fresh/assets/131708046/995b576c-235b-48ab-9c8d-83b0b53689ac)

- Model Training accuracy

![image](https://github.com/ddcots24/Hello-Fresh/assets/131708046/bd5e5574-844c-4f1a-8a5a-a5926a486e7b)

- Model test accuracy score was 99.8%

- Confusion Matrix

![image](https://github.com/ddcots24/Hello-Fresh/assets/131708046/3acef9e8-1da2-4f58-a22e-fddde01d8108)

### Evaluation
- Accuracy is very important instead of using just precision or a recall score because of the potential consequences.
  - If a piece of rotten beef is classified as fresh and then sent out to the consumer that could scar the reputation of HelloFresh.
  - On the other hand, if a fresh piece of meat is classified as rotten and thrown out, you are just pouring money down the drain.
  - Both sides of the coin are important and taken into consideration.
- Quality assurance for food is one of the first steps in an online food service business; to be able to streamline that with my model can be a time and money saver.

# **Quality assurance is also very important to uphold a companies reputation. Reputation is conveyed through customer reviews.**

## Text Classification
### Webscraping
- Scraped Trustpilot HelloFresh site.
- Scraped over 40,000 reviews.
- Manipulated data into positive and negative sentiments.
    - Positive sentiments were 4-5 star reviews.
    - Negative sentiments were 1-3 star reviews.
### Topic Modeling
- Ran a Non-negative Matrix Factorization Model to split the review text data into topics.
- Found the top 25 words in each topic.

![image](https://github.com/ddcots24/Hello-Fresh/assets/131708046/26cee01d-787b-4d13-979f-ea0f4d028d35)

- Gave each topic a label name.
    - Topic 1: Culinary experience
    - Topic 2: Delivery service
    - Topic 3: Recipe instructions
    - Topic 4: General

- Visualizing topic Segmentation

![image](https://github.com/ddcots24/Hello-Fresh/assets/131708046/5bded08e-1afc-44b0-baa7-9e2ae4de3115)

- The topics seem very segemented despite a little overlap with delivery service and culinary experience.
- I Incorporated this topic modeling as features for the Natural Language Process (NLP) modeling.

### Modeling
- Best model was a hyperparameter-tuned logistic regression model.
- Test accuracy score of 88%

Confusion Matrix

![image](https://github.com/ddcots24/Hello-Fresh/assets/131708046/4b6be2e5-7147-4c88-8c0d-56c0f9487df1)

ROC-AUC-Curve

![image](https://github.com/ddcots24/Hello-Fresh/assets/131708046/7a114206-d0c6-42a1-9e68-9ccc70a8d5b5)

AUC of 94%!!!

### Evaluation 
- Accuracy is the best metric because you want a balance in this situation. You do not want to classify negative sentiment as positive and vice versa.
- The model performed very well at predicting the positive class by making minimal errors. However, it made many mistakes predicting the positive class when the sentiment was negative.
    - I can infer that this happened because I included many 3-star or neutral sentiments in the negative class when reality some of those neutral sentiments had some positive notion. This can inherently confuse the model.
- In practicality, you can use this model to give positive or negative ratings to text reviews on websites that did not include stars in there ratings. You can also use this model to capture the sentiment of the text transcripts of phone calls and emails that don't use traditional review format.
