# AWS Cloud Cost Optimization - Identifying Stale Resources

## Identifying Stale EBS Snapshots

In this example, we'll create a Lambda function that identifies EBS snapshots that are no longer associated with any active EC2 instance and deletes them to save on storage costs.

### Description:

The Lambda function fetches all EBS snapshots owned by the same account ('self') and also retrieves a list of active EC2 instances (running and stopped). For each snapshot, it checks if the associated volume (if exists) is not associated with any active instance. If it finds a stale snapshot, it deletes it, effectively optimizing storage costs.



## Steps

1) Create EC2 Instance 
2) Check the volume attched to ec2 Instance and crate Snapshot out of that 
3) Go to Lambda Create new Function Runtime use python 3.10
4) Copy the Python code from the attched file paste in the Code source then Deploy and test will not work because we have not attached any IAM role 
6) so go to configration and permission click on role now create role to make this function work we need to list ec2 instance, EBS volume, and Snapshot describe and delete permission.

Refer this JSON code below to create IAM Policy 

```bash
  {
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "VisualEditor0",
			"Effect": "Allow",
			"Action": [
				"ec2:DescribeInstances",
				"ec2:DeleteSnapshot",
				"ec2:DescribeVolumes",
				"ec2:DescribeSnapshots"
			],
			"Resource": "*"
		}
	]
}
```
6) now go back to Lambda and test the code it will fail so in configration go to General configuration and edit the execution time to 10 sec and the default execution time is 3 sec.

7) now go back to ec2 instance and delete the instance it will automatically delete the volume as well howver Snapshot will remain.

8) Go back to Lambda and test the code it will delete the stale Snapshot or orphend Snapshot volume which is not associated to any instance.

## THANK YOU SO MUCH 



## Feedback

If you have any feedback, please reach out to  at roshanwaghmare92@gmail.com



