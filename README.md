# Argocd - test

My little repostitories to test argocd.

## Getting started

```
# Define the GOOGLE_PROJECT and GOOGLE_APPLICATION_CREDENTIALS environment variable.
Λ\: export GOOGLE_PROJECT=$(gcloud config get-value project)
Λ\: gcloud iam service-accounts keys create terraform-dev.json --iam-account terraform-dev@$GOOGLE_PROJECT.iam.gserviceaccount.com
Λ\: export GOOGLE_APPLICATION_CREDENTIALS=$PWD/terraform-dev.json
# OPTIONAL
Λ\: export GOOGLE_REGION=$(gcloud config get-value compute/region)
Λ\: export GOOGLE_ZONE=$(gcloud config get-value compute/zone)
# deploy infra and argocd
Λ\: infra/deploy.sh
Λ\: kubectl port-forward svc/argocd-server -n argocd 8080:443 &
```

The API server can then be accessed using the localhost:8080

The initial password is autogenerated to be the pod name of the Argo CD API server. This can be retrieved with the command [documentation](https://argoproj.github.io/argo-cd/getting_started/#4-login-using-the-cli)
```
Λ\: ARGOCD_PASS=`kubectl get pods -n argocd -l app.kubernetes.io/name=argocd-server -o name | cut -d'/' -f 2`
```

Default User : `admin`
