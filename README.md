# Getting Started

## Serverless 

![sta](https://user-images.githubusercontent.com/80678596/177031400-16a5fcba-224b-4835-893e-6e73743b40bc.png)

Your ability to delegate more of your operational duties to AWS and so increase your agility and innovation is made possible by serverless, which is the cloud's inherent architecture. You may create and execute apps and services using serverless technology without giving servers any thought. It does away with infrastructure management duties like capacity provisioning, operating system upkeep, server or cluster provisioning, and patching. Almost any backend service or application can be built with them, and everything needed to run and scale your application with high availability is taken care of for you.

## AWS Lambda

![sample-blank](https://user-images.githubusercontent.com/80678596/177030996-ef31daaf-8ef3-4370-af91-b05bb4d3c6ae.png)

You can run code with AWS Lambda without setting up or managing servers. There is no fee when your code is not executing; you only pay for the compute time you use.

You may use Lambda to run code for almost any kind of application or backend service with no administration required. Simply upload your code, and Lambda will handle all the necessary steps to run and grow it with high availability.


## Amazon API Gateway

![api-gateway](https://user-images.githubusercontent.com/80678596/177031280-4e4b0747-2213-4abf-81fc-8bc46e18b38e.png)


In order to construct, publish, maintain, monitor, and protect APIs at any size, developers can use the fully managed service known as Amazon API Gateway. It provides a complete framework for managing APIs. API Gateway manages traffic, permission and access control, monitoring, and API version management while enabling you to perform hundreds of thousands of API calls concurrently.

## Amazon DynamoDB

<img width="1861" alt="db" src="https://user-images.githubusercontent.com/80678596/177031324-b3bc4476-a2ee-4697-9aeb-76b29345acdf.png">

A consistent, single-digit millisecond latency at any scale is required by all applications, and Amazon DynamoDB provides a quick and adaptable NoSQL database service that can meet this need.

For internet-scale applications, it is a fully managed, multiregion, multimaster, persistent database with built-in backup and restore, security, and in-memory caching.

## Amazon S3

![s3](https://user-images.githubusercontent.com/80678596/177031215-0ad4013e-4111-4f29-a4e4-d916a9b8eec0.png)

Amazon Simple Storage Service is a cloud-based object storage service with industry-leading scalability, data availability, security, and performance. Amazon S3 is a simple web service interface that allows you to store and retrieve any amount of data from anywhere on the internet.

Customers of all sizes and industries can use it to store and protect any amount of data for a variety of use cases, including websites, mobile apps, backup and restore, archiving, enterprise applications, IoT devices, and big data analytics.

# Demo
<img width="1245" alt="Screenshot 2022-06-17 at 15 09 12" src="https://user-images.githubusercontent.com/80678596/174304587-9a1a282b-d0b5-40d2-8fc8-e26b33a1b493.png">  

# Serverless TODO

In this project I develop and deploy a simple "TODO" application using AWS Lambda and Serverless framework. This application will allow users to create/remove/update/get TODO items. Each TODO item contains the following fields: 
   - todoId (string) - a unique id for an item
   - createdAt (string) - date and time when an item was created
   -  name (string) - name of a TODO item (e.g. "Change a light bulb")
   - dueDate (string) - date and time by which an item should be completed
   - done (boolean) - true if an item was completed, false otherwise
   - attachmentUrl (string) (optional) - a URL pointing to an image attached to a TODO item

# Functions implemented

To implement this project you need to implement the following functions and configure them in the `serverless.yml` file:

* `Auth` - this function should implement a custom authorizer for API Gateway that should be added to all other functions.
* `GetTodos` - should return all TODOs for a current user. 
* `CreateTodo` - should create a new TODO for a current user. A shape of data send by a client application to this function can be found in the `CreateTodoRequest.ts` file
* `UpdateTodo` - should update a TODO item created by a current user. A shape of data send by a client application to this function can be found in the `UpdateTodoRequest.ts` file
* `DeleteTodo` - should delete a TODO item created by a current user. Expects an id of a TODO item to remove.
* `GenerateUploadUrl` - returns a presigned url that can be used to upload an attachment file for a TODO item. 

All functions are already connected to appriate events from API gateway

An id of a user can be extracted from a JWT token passed by a client

You also need to add any necessary resources to the `resources` section of the `serverless.yml` file such as DynamoDB table and and S3 bucket.


## Deploy Backend

                  cd backend

                  npm install
  
                  serverless

                  npm install --save-dev serverless-iam-roles-per-function@next 

                  serverless deploy --verbose


# Endpoints
   
  - GET - https://im1th8rr46.execute-api.us-east-2.amazonaws.com/dev/todos
  - POST - https://im1th8rr46.execute-api.us-east-2.amazonaws.com/dev/todos
  - PATCH - https://im1th8rr46.execute-api.us-east-2.amazonaws.com/dev/todos/{todoId}
  - DELETE - https://im1th8rr46.execute-api.us-east-2.amazonaws.com/dev/todos/{todoId}
  - POST - https://im1th8rr46.execute-api.us-east-2.amazonaws.com/dev/todos/{todoId}/attachment

functions:
  
# Lambda Functions

  - Auth: serverless-dev-Auth
  - GetTodos: serverless-dev-GetTodos
  - CreateTodo: serverless-dev-CreateTodo
  - UpdateTodo: serverless-dev-UpdateTodo
  - DeleteTodo: serverless-dev-DeleteTodo
  -  GenerateUploadUrl: serverless-dev-GenerateUploadUrl 
  
# Serverless 
  <img width="1438" alt="Screenshot 2022-06-17 at 14 52 03" src="https://user-images.githubusercontent.com/80678596/174301979-2bd3fe32-df87-4417-8f9c-88e7e43adbea.png">

  
  <img width="1440" alt="Screenshot 2022-06-17 at 14 50 52" src="https://user-images.githubusercontent.com/80678596/174301833-78e5a059-ad52-468b-ac52-ff371b130ed6.png">

  
# Auth0
  
 <img width="1440" alt="Screenshot 2022-06-17 at 14 53 08" src="https://user-images.githubusercontent.com/80678596/174302159-192628e6-ea03-4d56-9253-a22c349286d1.png">

  
# AWS Cloud Formation 

  <img width="1440" alt="Screenshot 2022-06-17 at 14 55 40" src="https://user-images.githubusercontent.com/80678596/174302538-4c3a2a21-321c-4a81-b143-5873c9c94c15.png">

   


# Frontend

The `client` folder contains a web application that can use the API that should be developed in the project.

To use it please edit the `config.ts` file in the `client` folder:

```ts
const apiId = '...' API Gateway id
export const apiEndpoint = `https://${apiId}.execute-api.us-east-1.amazonaws.com/dev`

export const authConfig = {
  domain: '...',    // Domain from Auth0
  clientId: '...',  // Client id from an Auth0 application
  callbackUrl: 'http://localhost:3000/callback'
}
```


# Suggestions

To store TODO items you might want to use a DynamoDB table with local secondary index(es). A create a local secondary index you need to a create a DynamoDB resource like this:

```yml

TodosTable:
  Type: AWS::DynamoDB::Table
  Properties:
    AttributeDefinitions:
      - AttributeName: partitionKey
        AttributeType: S
      - AttributeName: sortKey
        AttributeType: S
      - AttributeName: indexKey
        AttributeType: S
    KeySchema:
      - AttributeName: partitionKey
        KeyType: HASH
      - AttributeName: sortKey
        KeyType: RANGE
    BillingMode: PAY_PER_REQUEST
    TableName: ${self:provider.environment.TODOS_TABLE}
    LocalSecondaryIndexes:
      - IndexName: ${self:provider.environment.INDEX_NAME}
        KeySchema:
          - AttributeName: partitionKey
            KeyType: HASH
          - AttributeName: indexKey
            KeyType: RANGE
        Projection:
          ProjectionType: ALL # What attributes will be copied to an index

```

To query an index you need to use the `query()` method like:

```ts
await this.dynamoDBClient
  .query({
    TableName: 'table-name',
    IndexName: 'index-name',
    KeyConditionExpression: 'paritionKey = :paritionKey',
    ExpressionAttributeValues: {
      ':paritionKey': partitionKeyValue
    }
  })
  .promise()
```


## Deploy Frontend

To run a client application first edit the `client/src/config.ts` file to set correct parameters. And then run the following commands

```
cd client
npm install
npm run start
```

### Working Todo

  <img width="1260" alt="good-todo" src="https://user-images.githubusercontent.com/80678596/174300763-78ddd81d-0a0b-449e-9a4b-e84e769bfcc4.png">

### Blank Todo 
  <img width="1304" alt="blank-todo" src="https://user-images.githubusercontent.com/80678596/174301013-bf8430ad-3bbd-4a78-989c-b8d791f9cf71.png">



This should start a development server with the React application that will interact with the serverless TODO application.

