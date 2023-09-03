# SSM

[Reference](https://aws.amazon.com/blogs/mt/use-port-forwarding-in-aws-systems-manager-session-manager-to-connect-to-remote-hosts/)

Create a port forward to :3306 on a remote service via an SSM tunnel.

```shell
aws ssm \
  start-session \
  --target <ssm-managed-instance-id> \
  --document-name AWS-StartPortForwardingSessionToRemoteHost \
  --parameters '{"portNumber":["3306"],"localPortNumber":["1053"],"host":[" remote-database-host-name"]}'
```
