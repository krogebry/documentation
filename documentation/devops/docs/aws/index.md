# AWS specific things

```shell
aws sts get-caller-identity
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
for eip in $(aws ec2 describe-addresses --query 'Addresses[?AssociationId==null]'|jq -r '.[].AllocationId'); do aws ec2 release-address --allocation-id ${eip}; done
```
