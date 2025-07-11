# Bastion Builder 
# TODO: Write more readme



AMI Builder Required IAM permissions: 

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "ec2:CreateImage",
                "ec2:DescribeInstances",
                "ec2:ModifySnapshotAttribute",
                "ec2:CreateTags"
            ],
            "Resource": [
                "arn:aws:ec2:*:--myaccountnumber--:instance/*",
                "arn:aws:ec2:*::snapshot/*",
                "arn:aws:ec2:*::image/*"
            ]
        }
    ]
}
```


Bastion Builder Required IAM permissions: 
# Launch Instances from specifically tagged AMIs 
```json
{  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ReadOnlyAccess",
      "Effect": "Allow",
      "Action": [
        "ec2:Describe*",
        "ec2:GetConsole*",
        "cloudwatch:DescribeAlarms",
        "cloudwatch:GetMetricStatistics",
        "iam:ListInstanceProfiles"
      ],
      "Resource": "*"
    },
    {
      "Sid": "ActionsRequiredtoRunInstancesInVPC",
      "Effect": "Allow",
      "Action": "ec2:RunInstances",
      "Resource": [
        "arn:aws:ec2:us-east-1:AccountId:instance/*",
        "arn:aws:ec2:us-east-1:AccountId:key-pair/*",
        "arn:aws:ec2:us-east-1:AccountId:security-group/*",
        "arn:aws:ec2:us-east-1:AccountId:volume/*",
        "arn:aws:ec2:us-east-1:AccountId:network-interface/*",
        "arn:aws:ec2:us-east-1:AccountId:subnet/*"
      ]
    },
    {
      "Sid": "LaunchingEC2withAMIsAndTags",
      "Effect": "Allow",
      "Action": "ec2:RunInstances",
      "Resource": "arn:aws:ec2:us-east-1::image/ami-*",
      "Condition": {
        "StringEquals": {
          "ec2:ResourceTag/Environment": "Prod"
        }
      } 
    }
  ]
}
```
