# References

https://docs.openshift.com/container-platform/4.10/cicd/gitops/deploying-a-spring-boot-application-with-argo-cd.html

## AppSet
```yaml
apiVersion: argoproj.io/v1alpha1
kind: ApplicationSet
metadata:
  name: test-app-set
  namespace: openshift-gitops
spec:
  goTemplate: true
  goTemplateOptions: ["missingkey=error"]
  generators:
  - git:
      repoURL: 'https://github.com/DomenicoCutrupi/ArgoCD.git'
      revision: main
      directories:
      - path: esempio1/*
  template:
    metadata:
      name: '{{.path.basename}}'
      namespace: openshift-gitops
    spec:
      destination:
        namespace: test
        server: 'https://kubernetes.default.svc'
      project: default
      source:
        path: '{{.path.path}}'
        repoURL: 'https://github.com/DomenicoCutrupi/ArgoCD.git'
        targetRevision: main
```
