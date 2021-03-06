# Monitor Maintenance OU

## Description
This solution will provide an automated alerting system when an account is moved into the Maintenance OU. Maintenace OU typically has no or very permissive Service Control Policy, allowing for actions to be performed that are typically not allowed. Leaving an account in the Maintenance OU after compeleting required task introduces added risk while account is not under Control Tower guardrails. The solution uses a number of AWS services: Eventbridge Rule, Step Functions, Cloudwatch Alarm, SNS, Lambda

### Folder Structure

| Folder/File | Description |  
| :-------------------------| :-------------------------------------------------------------------------------------------------------------------|
| lambdas/stepfunctions/MaintenanceOuMonitorFn    | AWS Lambda Function that will check and alert if accounts are in Maintenance OU |
| scripts   | Directory that has the scripts that will be run to deploy the AWS Lambda Functions. |
| scripts/sam.sh   | Executes a number of SAM commands to package / build / deploy the SAM Function to a specified account. | 

## Pre-requisite Steps:
- Control Tower must be turned on in Management Account [Link to AWS Doc](https://docs.aws.amazon.com/controltower/latest/userguide/getting-started-with-control-tower.html)
- Install the Serverless Application Model CLI (SAM) [Link to AWS Doc](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html)
- Ensure you have AWS CLI and Console access to the AWS Management Account.
- SAM Bootstrap stack has been executed
- OU Named Maintenance created
- Existing SNS topic to send alerts (optional)

### Deploying Serverless Templates
These templates include the AWS StepFunction as well as all the Lambda Functions themselves.  The Lambda Function along 
with the CloudFormation to deploy them **cfn.yaml** are located in the "lambdas" directory.
- Deploy Serverless Application Model function.
  ```bash 
  ./scripts/sam.sh 
  ```
