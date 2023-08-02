# Hello-Fresh
## Business Understanding
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
- The image classification data comes from [Mendley Data](https://data.mendeley.com/datasets/nhs6mjg6yy/1).
- It has about 3000 images of raw beef; some being fresh and some being rotten.
- Some potential limitations are the amount of data I have; it could be more accurate with more training data.
- The text classification data I received comes from [Trustpilot](https://www.trustpilot.com/review/hellofresh.com). Trustpilot is an online review community that connects businesses and consumers through genuine feedback from customers about their buying and service experiences. 
- The raw data from Trustpilot is important because to be able to run a sentimental analysis, you need a good amount of reviews of text and a target.
- There are over 40,000 reviews which give me more than plenty of data to make a NLP model.
- Aside from the text, I used topic modeling to make the data more robust and try and find deeper underlying reasons.
## Beef Image Classification
### EDA
