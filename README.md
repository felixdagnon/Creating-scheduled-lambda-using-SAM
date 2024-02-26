# Creating-scheduled-lambda-using-SAM, Cloud9, Cloudwatch

We continuous with our last demo (Create-API-and-lambda-events-using-SAM)

Create scheduled lambda using SAM

We add additional resources from event souce types (github page)

In the template.yaml file, We are going to add additional resources from event souce types (github page) to obtain "lambda-events-schedule.yml" file

Here template.yaml file

```yml
Description: Test Pipeline Lambda
Resources:
  samfunction:
    Type: AWS::Serverless::Function
    Properties:
      Handler: hello_country.lambda_handler
      Runtime: python3.10
      CodeUri: samfunction
      Description: Sample SAM lambda deployment
    Metadata:
      SamResourceId: samfunction
```


Here is the final template for lambda-events-schedule.yml file

```yml
AWSTemplateFormatVersion: '2010-09-09'
Transform: 'AWS::Serverless-2016-10-31'
Description: Test Pipeline Lambda
Resources:
  hellofunction:
    Type: 'AWS::Serverless::Function'
    Properties:
      Handler: hello_country.lambda_handler
      Runtime: python3.10
      CodeUri: ./lambdacode/hello_country.py
      Description: Sample SAM Lambda Deployment
      Events:
        ScheduleEvent:
          Type: Schedule
          Properties:
            Schedule: rate(10 minutes)
```


![image](https://github.com/felixdagnon/Creating-scheduled-lambda-using-SAM/assets/91665833/ce4e9659-328d-4e43-82a8-08a7d046eaa0)



# Create scheduled lambda template with SAM

Let's run this package lambda-events-schedule.yml:

$ sam package --template-file lambda-events-schedule.yml --s3-bucket demotest-101 --output-template-file  lambda-events-schedule-packaged.yml




The pacckage is downloaded in SAM folder of Cloud9

![image](https://github.com/felixdagnon/Creating-scheduled-lambda-using-SAM/assets/91665833/48b1f1f2-c55e-4f41-b4f3-b940ec07f1d4)


Let's check s3 bucket

![image](https://github.com/felixdagnon/Create-API-and-lambda-events-using-SAM/assets/91665833/6338f502-f995-48cb-8617-3e459dca00e4)


# Deploying lambda package with SAM

To deploy the package run the below command

$ sam deploy --template-file lambda-events-schedule-packaged.yml --stack-name SAM-schedule-events --capabilities CAPABILITY_IAM

The package is done and changeset created in cloudformation

![image](https://github.com/felixdagnon/Creating-scheduled-lambda-using-SAM/assets/91665833/1dd07044-282a-4cc6-a7df-808449c281e5)

Let's see Cloudformation. The stack is created

![image](https://github.com/felixdagnon/Creating-scheduled-lambda-using-SAM/assets/91665833/f1425a61-da46-483f-be18-f0279bc2d4a9)

Let's check in lambda console

![image](https://github.com/felixdagnon/Creating-scheduled-lambda-using-SAM/assets/91665833/9bba735d-1651-46c7-91d4-b30dd8a56871)

Lambda deployment succeed

![image](https://github.com/felixdagnon/Creating-scheduled-lambda-using-SAM/assets/91665833/c21a9dee-efa3-446e-9d76-3e6ee4f5914d)

Click on cloudwatch event

![image](https://github.com/felixdagnon/Creating-scheduled-lambda-using-SAM/assets/91665833/91c4db1d-779e-472f-959e-0078c5b5209d)

lambda function is deployed

![image](https://github.com/felixdagnon/Creating-scheduled-lambda-using-SAM/assets/91665833/afc7ef61-0738-4d6a-86cb-ce7bfe6b9ad9)


