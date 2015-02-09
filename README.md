#How to use this code

1. Go to the AWS Lambda Console and create a new lambda function.
2. You'll need to setup two S3 buckets, one is the source that will trigger the lambda function and the other one is the destiny bucket where the auto-oriented photos will be stored.
3. You'll also need to setup two IAM Roles one for the bucket to be able to call the lambda function, and one for the lambda function to be able to read and write to the S3 buckets.

For a more detailed explanation check the AWS Lambda Walkthrough # 2 in which this handler is extraheavily based.

##Using the aws cli:

If you have never used the aws cli you'll need to install it and run `aws config`.

Then to zip the contents of this folder run `zip -r archive.zip ./*`

Then to upload the code:

		aws lambda upload-function \
		   --region us-east-1 \
		   --function-name ViuAutoOrient  \
		   --function-zip ./archive.zip \
		   --role arn:aws:iam::446362648863:role/lambda_exec_role_viu_autoorient \
		   --mode event \
		   --handler index.handler \
		   --runtime nodejs \
		   --debug \
		   --timeout 60 \
		   --memory-size 1024

Norice that:

__ViuAutoOrient__ is the name of the lambda function.
__lambda_exec_role_viu_autoorient__ is the name of the IAM Role with permissions to read and write from S3.
