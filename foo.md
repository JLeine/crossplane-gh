I also noticed that the ArgoCD Admin Password is somehow coming from [argo-cd.values](https://github.com/vfarcic/crossplane-gh/blob/main/argocd-values.yaml#L3) so I had to reset the password to gain access to the UI after port forwarding

```shell
kubectl -n argocd patch secret argocd-secret \            
  -p '{"data": {"admin.password": null, "admin.passwordMtime": null}}'
  
kubectl -n argocd rollout restart deployment argocd-server

kubectl -n argocd get secret argocd-initial-admin-secret \
  -o jsonpath="{.data.password}" | base64 -d
```

Not sure if that is intended?
