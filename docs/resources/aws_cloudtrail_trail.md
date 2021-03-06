---
title: About the aws_cloudtrail_trail Resource
---

# aws_cloudtrail_trail

Use the `aws_cloudtrail_trail` InSpec audit resource to test properties of a single AWS Cloudtrail Trail.

AWS CloudTrail is a service that enables governance, compliance, operational auditing, and risk auditing of your AWS account. With CloudTrail, you can log, continuously monitor, and retain account activity related to actions across your AWS infrastructure. CloudTrail provides event history of your AWS account activity, including actions taken through the AWS Management Console, AWS SDKs, command line tools, and other AWS services. This event history simplifies security analysis, resource change tracking, and troubleshooting.

Each AWS Cloudtrail Trail is uniquely identified by its trail_name or trail_arn.

<br>

## Syntax

An `aws_cloudtrail_trail` resource block identifies a trail by trail_name.

    # Find a trail by name
    describe aws_cloudtrail_trail('trail-name') do
      it { should exist }
    end

    # Hash syntax for trail name
    describe aws_cloudtrail_trail(trail_name: 'trail-name') do
      it { should exist }
    end

<br>

## Examples

The following examples show how to use this InSpec audit resource.

### Test that the specified trail does exist

    describe aws_cloudtrail_trail('trail-name') do
      it { should exist }
    end

### Test that the specified trail is encrypted using SSE-KMS

    describe aws_cloudtrail_trail('trail-name') do
      it { should be_encrypted }
    end

### Test that the specified trail is a multi region trail

    describe aws_cloudtrail_trail('trail-name') do
      it { should be_multi_region_trail }
    end

<br>

## Properties

### s3_bucket_name

Specifies the name of the Amazon S3 bucket designated for publishing log files.

    describe aws_cloudtrail_trail('trail-name') do
      its('s3_bucket_name') { should cmp "s3-bucket-name" }
    end

### trail_arn

The ARN identifier of the specified trail. An ARN uniquely identifies the trail within AWS.

    describe aws_cloudtrail_trail('trail-name') do
      its('trail_arn') { should cmp "arn:aws:cloudtrail:us-east-1:484747447281:trail/trail-name" }
    end

### cloud_watch_logs_role_arn

Specifies the role for the CloudWatch Logs endpoint to assume to write to a user\'s log group.

    describe aws_cloudtrail_trail('trail-name') do
      its('cloud_watch_logs_role_arn') { should include "arn:aws:iam:::role/CloudTrail_CloudWatchLogs_Role" }
    end

### cloud_watch_logs_log_group_arn

Specifies a log group name using an Amazon Resource Name (ARN), a unique identifier that represents the log group to which CloudTrail logs will be delivered.

    describe aws_cloudtrail_trail('trail-name') do
      its('cloud_watch_logs_log_group_arn') { should include "arn:aws:logs:us-east-1::log-group:test:*" }
    end

### kms_key_id

Specifies the KMS key ID to used to encrypt the logs delivered by CloudTrail. 

    describe aws_cloudtrail_trail('trail-name') do
      its('kms_key_id') { should include "key-arn" }
    end

### home_region

Specifies the region in which the trail was created.

    describe aws_cloudtrail_trail('trail-name') do
      its('home_region') { should include "us-east-1" }
    end


## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers (such as `exist`) please visit our [matchers page](https://www.inspec.io/docs/reference/matchers/).

### be_multi_region_trail

The test will pass if the identified trail is a multi region trail.

    describe aws_cloudtrail_trail('trail-name') do
      it { should be_multi_region_trail }
    end

### be_encrypted

The test will pass if the logs delivered by the identified trail is encrypted.

    describe aws_cloudtrail_trail('trail-name') do
      it { should be_encrypted }
    end

### be_log_file_validation_enabled

The test will pass if the identified trail has log file integrity validation is enabled.

    describe aws_cloudtrail_trail('trail-name') do
      it { should be_log_file_validation_enabled }
    end
