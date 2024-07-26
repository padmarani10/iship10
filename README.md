1. Create the S3 Bucket
aws s3api create-bucket --bucket ishipbuck-10 --region us-west-2 --create-bucket-configuration LocationConstraint=us-west-2


2. Configure Object Ownership
aws s3api put-bucket-ownership-controls --bucket ishipbuck-10 --ownership-controls Rules=[{ObjectOwnership=BucketOwnerPreferred}]

3. Enable Bucket Versioning
aws s3api put-bucket-versioning --bucket ishipbuck-10 --versioning-configuration Status=Enabled

4. Enable Static Website Hosting
Create a file named website-configuration.json with the following content:

{
  "IndexDocument": {
    "Suffix": "index.html"
  },
  "ErrorDocument": {
    "Key": "error.html"
  }
}

aws s3api put-bucket-website --bucket ishipbuck-10 --website-configuration file://webbuck.json


5. Command to Turn Off Block All Public Access

aws s3api put-public-access-block \
    --bucket ishipbuck-10 \
    --public-access-block-configuration \
    '{
      "BlockPublicAcls": false,
      "IgnorePublicAcls": false,
      "BlockPublicPolicy": false,
      "RestrictPublicBuckets": false
    }'

6. Grant Public Read Access to the Bucket : Set Bucket ACL to Public Read
aws s3api put-bucket-acl --bucket ishipbuck-10 --acl public-read

7. upload files to s3 bucket
aws s3 cp index.html s3://ishipbuck-10 --acl public-read
aws s3 cp courses.html s3://ishipbuck-10 --acl public-read
aws s3 cp about.html s3://ishipbuck-10 --acl public-read
aws s3 cp contact.html s3://ishipbuck-10 --acl public-read
aws s3 cp protfolio.html s3://ishipbuck-10 --acl public-read
aws s3 cp pricing.html s3://ishipbuck-10 --acl public-read

8.To uplload floders to the s3 bucket
aws s3 cp js s3://ishipbuck-10/js --recursive --acl public-read
aws s3 cp css s3://ishipbuck-10/css --recursive --acl public-read
aws s3 cp img s3://ishipbuck-10/img --recursive --acl public-read
aws s3 cp fonts s3://ishipbuck-10/fonts --recursive --acl public-read

9.End point 
http://ishipbuck-10.s3-website-us-west-2.amazonaws.com


