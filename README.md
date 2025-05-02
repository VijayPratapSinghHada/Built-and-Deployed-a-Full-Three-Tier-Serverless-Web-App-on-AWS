<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Three-Tier Web App

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-threetier)

**Author:** Vijay Pratap Singh Hada  
**Email:** vijaypratapsinghhada9@gmail.com

---

## Build a Three-Tier Web App

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-compute-threetier_2b3c4d5e)

---

## Introducing Today's Project!

In this project, I will demonstrate how to build a three-tier web app from scratch. I will first create the presentation layer, followed by setting up the logic layer, and finally establishing the data layer. This project allows me to learn how to construct a three-tier web app step by step, understand how each component works together, discover best practices for web development, and gain mastery of AWS compute services.

### Tools and concepts

Services I used were Amazon S3 for storage, CloudFront for content delivery, API Gateway for managing API requests, Lambda functions for serverless logic, and DynamoDB for database management. Key concepts I learned include Lambda functions for executing code without managing servers, CORS for enabling secure requests between different origins, and how to integrate multiple AWS services to build a scalable web application. 

### Project reflection

This project took me approximately 3 hours and 45 minutes to complete. The most challenging part was solving the browser error related to the PROD URL, as it required careful troubleshooting. It was most rewarding to see my website working correctly, with data being retrieved successfully and displayed as intended. 

I did this project today to strengthen my understanding of AWS services and three-tier architecture. It met my goals by providing hands-on experience in building a scalable web application and troubleshooting common issues.




---

## Presentation tier

For the presentation tier, I will set up the main layer that users see when they visit the website. First, I will create an S3 bucket, which will store files for the website, including an `index.html` file. Then, I will set up CloudFront to quickly deliver this content globally, using servers located all around the world. This is important because the presentation tier handles website files and spreads them efficiently over the internet, ensuring users can access the site quickly and easily. 

I accessed my delivered website by visiting the CloudFront distribution URL. This URL works well because CloudFront caches my website content across various locations worldwide, allowing users to load the website quickly. Additionally, I set up Origin Access Control (OAC), which ensures that the S3 bucket only allows access through the CloudFront distribution, keeping my files secure. This setup improves both speed and security for my website.

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-compute-threetier_3a4b5c6d)

---

## Logic tier

For the logic tier, I will set up a Lambda function that manages requests and fetches data from a DynamoDB table. Additionally, I will use API Gateway to receive requests from users and direct them to the appropriate Lambda function. This setup is essential because the Lambda function handles data retrieval, while API Gateway helps manage the flow of requests, ensuring everything works smoothly together.

The Lambda function retrieves data by using the user ID provided in the request to look up information in the DynamoDB table. It sends a request to DynamoDB with this user ID and checks if the data exists. If found, the function returns the user data; if not, it returns an error message. This process allows the function to efficiently access and deliver the required information to users.

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-compute-threetier_6a7b8c9d)

---

## Data tier

For the data tier, I will set up a DynamoDB table to store user data because this tier is responsible for holding all the information that the application needs. DynamoDB is a flexible and scalable database service that allows us to easily manage and retrieve data. By using it, our three-tier web application can store user information securely and access it efficiently whenever needed.

The partition key for my DynamoDB table is `userId`, which means that when the table searches for user data, it will do so based on the `userId`. This ensures that each user’s information can be quickly accessed by their unique ID. When the table is queried, it will return all the relevant data associated with that specific `userId`, making it efficient for retrieving user-related information. 

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-compute-threetier_u1v2w3x4)

---

## Logic and Data tier

Once all three layers of my three-tier architecture are set up, the next step is to connect them. First, I will update the `index.html` file to send a request to the API Gateway endpoint, which will get data and return it to the user. Additionally, I will modify the `script.js` file to make the actual API request. This integration will ensure that the user can access the data stored in the database through the web application smoothly. 

To test my API, I went to the API Gateway console, accessed the prod stage, and copied the Invoke URL. I then appended `/users?userId=1` to the end of the URL and ran it in my web browser. The results showed a response containing the item data for the specified user ID. This confirmed that both the logic and data tiers are functioning properly in the three-tier architecture. 

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-compute-threetier_a112c3d5)

---

## Console Errors

The error in my distributed site was because I hadn't provided the PROD stage API URL in the `script.js` file. This URL is essential for connecting my web application to the API Gateway, allowing it to retrieve user data. Without the correct URL, the application cannot access the backend logic needed to fetch and display the requested information. Updating this URL should resolve the issue and enable the site to function properly. 

To resolve the error, I updated script.js by replacing the placeholder with the actual PROD API URL using my code editor on my local machine. I then reuploaded it to S3 because the API Gateway needs the correct URL to respond to user requests. This update will enable the application to access the necessary data and function properly for users.




I ran into a second error after updating `script.js`. This was a CORS (Cross-Origin Resource Sharing) error because the API Gateway wasn't configured to allow requests from my CloudFront URL. By default, browsers block requests coming from different domains for security reasons. To fix this, I need to enable CORS on the API Gateway, which will allow my CloudFront-hosted site to communicate with the API and access the necessary data. 

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-compute-threetier_a1b2c3d5)

---

## Resolving CORS Errors

To resolve the CORS error, I first navigated to the API Gateway console and selected the `/users` resource. I then enabled CORS and checked both GET and OPTIONS under Access-Control-Allow-Methods. Next, I entered my CloudFront distribution domain name as the Access-Control-Allow-Origin value. This configuration allows requests from my CloudFront site to communicate with the API, fixing the CORS issue and enabling proper data access. 

I also updated my Lambda function because I needed to ensure that it supports CORS by returning the proper headers in the response. The changes I made included adding the `Access-Control-Allow-Origin` header to allow requests from my CloudFront domain. This ensures that my API can be accessed securely from my frontend, resolving any CORS issues and allowing data retrieval to work correctly. Additionally, I confirmed that I replaced the placeholder with my actual AWS region code "ap-south-1" for proper functionality. 

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-compute-threetier_1qthryj2)

---

## Fixed Solution

I verified the fixed connection between API Gateway and CloudFront by refreshing my CloudFront domain in the browser. After making the necessary updates to support CORS and ensuring the Lambda function returned the correct headers, I checked to see if the data from DynamoDB was displayed on my website. The successful retrieval of data confirmed that everything was working properly!

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-compute-threetier_2b3c4d5e)

---

---
