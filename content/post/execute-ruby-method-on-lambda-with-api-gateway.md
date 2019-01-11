---
title: "Execute a Ruby Method on Lambda With Api Gateway"
date: 2019-01-11T10:30:36-05:00
draft: false
---

Amazon now offers Ruby 2.5 Lambda functions! I was able to take advantage of this at my job. Lambda functions are great when you want to periodically run a script or do some stateless work. In the past, I have created Node and Python functions to pull data, send emails and push data to external API's. In this post, I explore how I use the Ruby implementation of Lambda in order to verify if a URL is valid.

Writting this function is Lambda has many advantages that include:

1. Not having to bear the cost of maintaining software
1. Lambda is super cheap in my use case

### What is Needed?

#### Create Lambda and Connect API Gateway

1. Create a Ruby 2.5 Lambda function
1. Under "Add triggers", click "API Gateway"
1. Choose API -> Create a new API
1. Choose Security -> Open
1. Click "Add" button

#### Test Basic Setup
```ruby
def lambda_handler(event:, context:)
  { statusCode: 200, body: JSON.generate("Hello!") }
end
```

You should be able to visit the URL provided by the API Gateway and view the text "Hello".


#### Lambda Parameter Consumption

1. Go to the API Gateway service
1. Go to the gateway hooked up to the lambda function
1. Under "Actions", click "Create Method"
1. Click on "GET"
1. Under "Integration Request", click "Lambda Function"
1. Click to reveal "Mapping Templates"
1. Click "When there are no templates defined (recommended)" radio
1. Add mapping template and set value to "application/json"
1. Generate template "Method Request passthrough"
1. Click "Save" button

- Now, all the request data will be forwarded to the Lambda function
- This means, we can pass a url param in the on the API Gateway which is consumed in the Lambda function

The final Lambda function is:
```ruby
def lambda_handler(event:, context:)
  url = event.dig('params', 'querystring', 'url')

  valid = UrlValidator.valid?(url)
  { statusCode: 200, body: JSON.generate({valid: valid}) }
end
```

#### Debugging
In order to get the function working, I relied on the method test functionality provided by the API Gateway. On one tab, I had the Lambda code open. While in another tab, I had the client test. 

You can find the test functionality by clicking the "GET" route, then clicking

![this image](/post/images/test_lightning.png)

In order to the the `url` param:

1. On the {urlValidator} text input enter, "url=whatever"
1. Click the test button and see the results of running the Lambda function!


