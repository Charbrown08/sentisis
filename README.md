# Observability Infrastructure

Este proyecto implementa una infraestructura de observabilidad utilizando Terraform, AWS y Docker. Incluye la configuración de Prometheus, Grafana y Node Exporter para monitorear métricas del sistema.

## Descripción

La infraestructura incluye:
- Una instancia EC2 en AWS configurada con Docker.
- Prometheus para recopilar métricas.
- Grafana para visualizar las métricas.
- Node Exporter para exponer métricas del sistema.

## Configuración

### Variables principales
El archivo [`variables.tf`](terraform/variables.tf) define las variables necesarias para desplegar la infraestructura, como la región de AWS, el tipo de instancia, y el ID de la AMI.

### Scripts
El script [`userdata.sh`](scripts/userdata.sh) configura automáticamente la instancia EC2 para instalar y ejecutar Docker, Prometheus, Grafana y Node Exporter.

### Módulos
Se utilizan módulos para:
- Gestionar roles y políticas de IAM ([`iam-role-secrets`](terraform/modules/iam-role-secrets)).
- Configurar Secrets Manager para almacenar credenciales de Grafana ([`secrets-manager`](terraform/modules/secrets-manager)).

## Evidencia

A continuación, se muestra una captura de pantalla de la interfaz de Grafana con las métricas de CPU y RAM:

![Grafana Dashboard](https://user-images.githubusercontent.com/your-image-path/grafana-dashboard.png)

## Cómo desplegar

1. Configura las variables en [`staging.tfvars`](terraform/envs/staging.tfvars).
2. Ejecuta los siguientes comandos:
   ```bash
   terraform init
   terraform apply -var-file=terraform/envs/staging.tfvars