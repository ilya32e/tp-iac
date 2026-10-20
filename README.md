# TP Jour 3 — Terraform et GitLab CI/CD

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

## GitHub Actions

Le workflow [.github/workflows/terraform.yml](.github/workflows/terraform.yml)
remplace le pipeline GitLab pour GitHub. Il exécute la validation Terraform,
puis affiche la variable `APP_ENV`.

Dans GitHub, créer une variable de dépôt `APP_ENV` dans **Settings → Secrets
and variables → Actions → Variables**, avec la valeur `production`.
