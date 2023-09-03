# AWS specific things

```shell
aws sts get-caller-identity
```

## ECR Login

```shell
aws ecr get-login-password | docker login --username AWS --password-stdin AWS_ACCOUNT_ID.dkr.ecr.us-east-1.amazonaws.com
```

#### Alias

```shell
alias ecr_login="aws ecr get-login-password | docker login --username AWS --password-stdin AWS_ACCOUNT_ID.dkr.ecr.us-east-1.amazonaws.com"
```


## Find latest AMI

```shell
aws ec2 describe-images --owners 1234 --filters "Name=name,Values=ubuntu-20.04-20230208221620"  
```

## Add up the EBS volumes that are unattached.

```shell
aws ec2 describe-volumes --filters "Name=status,Values=available" | jq '[.Volumes[].Size|tonumber]|add'
```

## Get unattached EIPs

```shell
aws ec2 describe-addresses --query 'Addresses[?AssociationId==null]'|jq '.[].AllocationId'
```

## Cleanup EIPs

```shell
for eip in $(aws ec2 \
  describe-addresses \
  --query 'Addresses[?AssociationId==null]'|jq -r '.[].AllocationId'); do aws ec2 release-address --allocation-id ${eip}; done
```

## Get latest

[Reference](https://docs.aws.amazon.com/eks/latest/userguide/retrieve-ami-id.html)

```shell
aws ssm \
  get-parameter \
  --region us-east-1 \
  --query "Parameter.Value" \
  --output text \
  --name /aws/service/eks/optimized-ami/1.27/amazon-linux-2/recommended/image_id
```

Result: `ami-013895b64fa9cbcba`

