# terraform

Terraform + IaC — infraestructura como código

## Idea

Base para gestionar infraestructura cloud con Terraform. Estado remoto, módulos reutilizables, y separación por entornos. Agnóstico del provider (AWS, GCP, Azure) con ejemplos para el más común (AWS).

## Stack

- **Terraform 1.9+** — IaC tool de HashiCorp
- **AWS Provider** — (intercambiable por GCP/Azure)
- **S3 + DynamoDB** — remote state y state locking
- **Terragrunt** (opcional) — DRY config entre entornos
- **tflint** — linting de Terraform
- **checkov** — security scanning de IaC

## Structure

```
modules/              # Módulos reutilizables (no tienen estado propio)
  vpc/
    main.tf
    variables.tf
    outputs.tf
    README.md
  ecs-service/
  rds/
environments/         # Un directorio por entorno
  dev/
    main.tf           # Llama a módulos con vars de dev
    variables.tf
    outputs.tf
    terraform.tfvars  # Valores concretos (no secrets)
    backend.tf        # Config del remote state
  staging/
  prod/
.terraform.lock.hcl   # Lock de versiones de providers
.tflint.hcl
```

## Decisions

- Módulos en `modules/` son reutilizables y no tienen backend — solo resources + variables + outputs.
- Cada entorno tiene su propio state — nunca un state compartido entre dev y prod.
- Remote state en S3 con locking en DynamoDB — evita corrupción por ejecuciones paralelas.
- Secrets via Variables de entorno (`TF_VAR_`) o AWS Secrets Manager — nunca en `.tfvars`.
- `terraform fmt`, `terraform validate`, y `tflint` en CI antes de `plan`.
