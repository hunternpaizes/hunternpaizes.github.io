# Deployment Guide (Draft)

## Overview
The Super Data Viewer platform supports both standalone and Kubernetes-based deployments. This guide outlines recommended practices for each environment, focusing on reproducibility, security, and observability.

## Prerequisites
- Docker Engine 24+ and Docker Compose 2+ for standalone deployments.
- Access to a Kubernetes cluster (v1.26+) with Helm 3 for distributed deployments.
- Container registry credentials for pulling/pushing project images.
- HashiCorp Vault or compatible secret management solution.
- External object storage (e.g., S3, Azure Blob) when working with large datasets.

## Standalone Deployment (Docker Compose)
1. Clone the deployment repository and copy the provided `.env.example` to `.env`.
2. Populate environment variables for database credentials, JWT secrets, Vault tokens, and external service URLs.
3. Run `docker compose up -d` to build and launch the API, worker, frontend, database, and monitoring containers.
4. Access the application at `https://localhost:8443` (reverse proxy terminates TLS using provided certificates).
5. Use `docker compose logs -f` for troubleshooting and `docker compose down` to stop the stack.

## Cluster Deployment (Kubernetes + Helm)
1. Ensure cluster-level ingress, storage classes, and certificate management (e.g., cert-manager) are configured.
2. Add the Helm repository or package charts locally: `helm repo add super-data-viewer https://example.com/charts`.
3. Create a dedicated namespace: `kubectl create namespace sdv`.
4. Install dependencies such as PostgreSQL/TimescaleDB, Redis (optional), and object storage gateways via Helm or managed services.
5. Deploy the platform:
   ```bash
   helm install sdv super-data-viewer/platform \
     --namespace sdv \
     --values values.yaml
   ```
6. Configure `values.yaml` with image tags, replica counts, resource requests/limits, ingress hosts, TLS secrets, and Vault integration settings.
7. Verify readiness with `kubectl get pods -n sdv` and review logs using `kubectl logs`.
8. Set up autoscaling policies for API pods and Celery workers based on CPU utilization or queue depth.

## Configuration & Secrets
- Store sensitive values (database passwords, API keys, SMTP credentials) in Vault and inject them via Kubernetes secrets or environment variables.
- Maintain separate configuration overlays for development, staging, and production.
- Rotate secrets periodically and audit access through Vault policies.

## Observability Setup
- Deploy Prometheus and Grafana using the bundled Helm dependencies or existing monitoring stack.
- Configure service monitors to scrape API and worker metrics.
- Forward application logs to OpenSearch or a compatible log store via Fluent Bit/Vector sidecars.
- Set up Alertmanager routes for email, SMS, or webhook notifications on critical alerts.

## Backup & Disaster Recovery
- Schedule database snapshots and object storage lifecycle policies.
- Export configuration, Helm values, and Vault policies to version control.
- Test restore procedures regularly to validate RPO/RTO objectives.

## Post-deployment Tasks
- Create the initial administrator account and verify email delivery.
- Register organizational domains for single sign-on (optional).
- Populate sample datasets and pipelines to validate end-to-end functionality.

## Maintenance
- Track image vulnerabilities with container scanning tools and apply security patches promptly.
- Perform rolling upgrades by bumping Helm chart versions; use blue/green strategies for major changes.
- Monitor system capacity and adjust resource allocations as workloads evolve.
