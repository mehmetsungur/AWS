# Event Driven App with SQS-Lambda-DynamoDB

## Step 1: Make sure yo are in us-east-1 (N.Virginia)


## Step 2: Create DynamoDB Table

Name: ProductVisits
Partition key: ProductVisitKey

Leave the rest as default.

## Step 3: Create SQS Queue

Name: ProductVisitsDataQueue
Type: Standard

Leave the rest as default.

Copy the **Queue URL** after creation.

## Step 4: Create Lambda Function

Author from scratch
Name: productVisitsDataHandler
Runtime: Node.js 12.x
Role: create new role from AWS policy templates
Role name: lambdaRoleForSQSPermissions
Add policy templates: "Simple microservice permissions" and "Amazon SQS poller permissions"

## Step 5: Upload Lambda Function Code

From "Upload from" menu in front of function code heading upload the zip file lambda-nodejs.zip

## Step 6: Test Messsaging

Go to AWS CLI and send messages:
    AWS CLI Command: `aws sqs send-message --queue-url https://sqs.us-east-1.amazonaws.com/938251564890/ProductVisitsDataQueue --message-body file://message-body-1.json`
    Modify: Queue name and file name

Go back to SQS and open "ProductVisitsDataQueue"

Find Send and Receive Messages and Click
Click Poll for messages to receive messages, then check the message body

## Step 7: Configure SQS

Go back to "ProductVisitsDataQueue"

Configure Lambda function trigger and specify Lambda function:
Name: productVisitsDataHandler

Go to Send and Receive Messages
Click Poll for messages again
This time, no messages appear

## Step 8: Check DynamoDB for messages

Click Explore Items to see if there are any items in the ProductVisits table

## Step 9: Use AWS CLI to send messages to SQS

Go to AWS CLI and send all of the messages from 1 to 5:
    AWS CLI Command: `aws sqs send-message --queue-url https://sqs.us-east-1.amazonaws.com/244392073887/ProductVisitsDataQueue --message-body file://message-body-1.json`

    (Modify: Queue name and file name)

## Step 10: See Cloudwatch Logs

Go to Cloudwatch and find Log groups
find the name of the Lambda function
see the blocks that begin with START and finish with END
