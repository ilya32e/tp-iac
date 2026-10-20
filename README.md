# TP Jour 3

## Infrastructure

Le projet provisionne localement avec Docker :

- l'image `nginx:latest` ;
- le réseau `tp3-network` ;
- le conteneur `tp3-web`, accessible sur le port `8081`.

Commandes principales :

```powershell
terraform init
terraform fmt -check
terraform validate
terraform plan
terraform apply
terraform state list
terraform graph
```

Pour vérifier le site : `Invoke-RestMethod http://localhost:8081`.
