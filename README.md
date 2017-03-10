# aws-lambdas

[![Build Status](https://travis-ci.org/kyhau/aws-lambdas.svg?branch=master)](https://travis-ci.org/kyhau/aws-lambdas)

My AWS Lambda functions for personal use.

## Scripts being run through Lambda
    
1. `EC2/autostop_ec2/autostop-ec2`
    - Autostop EC2 instances with specified tag

1. `EC2/autostop_ec2/reset-autostop-ec2`
    - Reset Autostop tags of specific EC2 instances

1. `EC2/backup_ec2/create-ec2-backups`
    - Create AMI and Snapshot(s) for EC2 instance
    - Managed by role: Lambda-EC2-Snapper

1. `EC2/backup_ec2/tag-ec2-backups`
    - Tag Snapshots of AMI of EC2 instance
    - Managed by role: Lambda-EC2-Snapper

1. `EC2/backup_ec2/delete-ec2-backups`
    - Delete expired backup (AMI and the corresponding Snapshots)
    - Managed by role: Lambda-EC2-Snapper

### How the scripts are used

These scripts are intended to be run as AWS Lambda jobs triggered by
an AWS CloudWatch scheduled event. They can also be run from
command line or from crontab.


#### Run from AWS Lambda

Lambda is a code execution service offered by Amazon Web Services.
When you configure a single Lambda behavior, it runs based on events
you specify **without needing a server of any kind**.

1. Create an AWS IAM Role that allows the AWS Lambda service to call
AWS services (e.g. Lambda-EC2-Snapper).

1. Create a new AWS Lambda function with the contents of
create-ec2-backups.py. Configure the DEFAULTS as appropriate for your
environment.

1. Add a new CloudWatch Schedule Trigger for the Lambda function
at the interval you require.

4. Wait for CloudWatch to trigger the scheduled event or use the
AWS Lambda "Test" button to run manually.


#### Run from Command Line

1. Set up AWS configure to store your Access Key ID and 
   Secret Access Key in `~/.aws`. See ["Configuring the AWS Command 
   Line Interface"](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html) 
   for more details.

1. Change `profile_name` and `DEFAULTS` in the __main__ of the scripts

1. Build

```cmd
virtualenv env
. env/bin/activate    (on linux; or env\Scripts\activate on Windows)
pip install -r requirements.txt

```
