# Overview

Using `go` to test helm charts.

``` mermaid
graph LR
  A[Start] --> B[Lint];
  B --> Deploy[Deploy to K8s];
  Deploy --> Test[Test];
  Test --> GoTest[go test];
  Test --> KubeScore[kube-score];
  Test --> SecurityScan[wiz scan];
  GoTest --> Publish[Publish to art];
  KubeScore --> Publish;
  SecurityScan --> Publish;
```
