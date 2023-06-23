import json
import boto3
def lambda_handler(event, context):
    sns = boto3.client('sns')
    finding = event['detail']['findings'][0]
    message = json.dumps(finding, indent=4)
    response1 = sns.publish(
        TopicArn='arn:aws:sns:us-west-2:705235841658:Accounting1',
        Message=message
    )
    response2 = sns.publish(
        TopicArn='arn:aws:sns:us-west-2:705235841658:Accounting2',
        Message=message
    )
    response3 = sns.publish(
        TopicArn='arn:aws:sns:us-west-2:705235841658:EC2-Instance-State',
        Message=message
    )
    return response1, response2, response3
