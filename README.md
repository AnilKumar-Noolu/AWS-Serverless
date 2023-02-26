# AWS-Serverless

In this Repo, I will use event-driven architectures to decouple distributed applications.
I will configure an Amazon Simple Storage Service(Amazon S3) Bucket to invoke an Amazon SNS Notification whenever an Object is added to an S3 Bucket.
The services we used in AWS are S3, SQS, SNS amd AWS Lambda.

The process flow is:
1) You upload an Image file to Amazon S3 bucket.
2)Uploading the file to bucket invokes an event notification to the SNS Topic.
3)Amazon SNS then distributes the notification to Amazon SQS queues.
4)The Lambda function process the images (resizes) and stores the output in S3 Bucket.
5)You validate the processed images in S3 bucket folder and logs in Amazon CloudWatch.

STEPS:
-> Create an Amazon Standard SNS Topic and Note Down the ARN name and Topic Owner.
-> Create an Amazon SQS Queue and subscribe that to SNS Topic and also check whether they both are interconnecting by publishing messages in SNS.
-> Configure the SNS acess policy to allow S3 bucket to publish to a topic.
-> Click on selecetd SNS Topic -> Edit-> Navigate to access policy and copy the mentioned data in the repo.
-> Replace the Trusted Owner Value and Topic-ARN in the SNS_access_policy code attached.
-> Create a S3 Bucket and create a proper event Notification for that bucket with "All object create events" and destination as SNS Topic created before.

-> Now create an AWS Lambda Function with SQS Trigger that reads an image from S3 Bucket, resize that image and stores that into new S3 Bucket.
-> Create a new function with Python-3.7 runtime and Role which contains both S3 and SNS access.
->After creating Lambda function, add a trigger of SQS to it.
-> In the code section, add the required code in .zip format, and also edit handler and Configuration -> general Configuration also.

-> Now, when a file is added to the S3 Bucket under specified folder, Laambda process that and resizes that file and again uploads that to another new bucket as mentioned in the code specified in Lambda code. You can verify the process by adding a file in S3 Bucket and checking the resized images in another bucket.

-> Also you can create the LifeCycle Configuration to delete files in the S3 Bucket after some specified days.
