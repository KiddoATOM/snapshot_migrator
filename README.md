# snapshot-migrator.sh 

Script to migrate last snapshot of volume in a region to another region.

## Important
In the first lines of the script the LOG PATH is set. Default: "/var/log/snashot-copy"
The script creates the folder if not exists but you need to run the script as sudo.
Is will be better practice if you create the script and set the owner to the folder as the same that will be used to run the script.

## Usage

```bash
sudo bash test.sh -s source-region -t target-region -v source-volume-id
``` 

Example:
```bash 
sudo bash test.sh -s us-west-2 -t us-west-1 -v vol-0c96b61b89fa48a83
``` 

## Inputs
| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| -s | Snapshot source region | string | | yes |
| -t | Region where the snapshot will be copied | string | | yes |
| -v | Volume ID of the snapshot that will be copied | string | | yes |

## AWS permission 

If you run this script in an AWS instance you neet to attach this policy to the role of the instance.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "ec2:CopySnapshot",
                "ec2:DeleteSnapshot",
                "ec2:CreateTags",
                "ec2:CreateSnapshots",
                "ec2:DescribeSnapshots"
            ],
            "Resource": "*"
        }
    ]
}
```