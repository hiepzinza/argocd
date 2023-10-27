# ArgoCD


```
---
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: myapp
  namespace: argocd
  annotations:
    argocd-image-updater.argoproj.io/image-list: hiepdxzinza/nginx:~v0.1
  # finalizers:
  #   - resources-finalizer.argocd.argoproj.to
spec:
  project: default
  source:
    repoURL: https://github.com/hiepzinza/argocd.git
    targetRevision: main
    path: helm
    helm:
      parameters:
        - name: "image.repository"
          value: hiepdxzinza/nginx
        - name: "image.tag"
          value: v0.1.0
  destination:
    server: https://kubernetes.default.svc
    namespace: myapp
```