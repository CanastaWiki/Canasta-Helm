# Canasta Helm Chart

This repository hosts the Helm chart for a classic [Canasta](https://github.com/CanastaWiki/Canasta) stack.

## Usage

1. Add the repository:
   ```bash
   helm repo add canasta https://canastawiki.github.io/Canasta-Helm/
   helm repo update
   ```

2. Install the chart:
   ```bash
   helm install my-canasta canasta/canasta
   ```

## Configuration

See [values.yaml](values.yaml) for default configuration values.

### Automated Installation
For fresh installations, the chart can automatically install MediaWiki and generate `LocalSettings.php`. This is enabled by default.

You can configure the installation parameters in `values.yaml`:

```yaml
install:
  enabled: true
  siteName: "CanastaWiki"
  adminUser: "admin"
  adminPassword: "password" # IMPORTANT: Change this!
  dbUser: "root"
  dbPassword: "mediawiki"
  lang: "en"
```

The generated `LocalSettings.php` will be stored in the persistent volume (`config-data`), so it survives pod restarts.

### Persistence
By default, the chart uses PVCs. For local development (e.g., Minikube/Docker Desktop) where you want to mount local directories, you can use `hostPath`:

```bash
helm install my-canasta canasta/canasta \
  --set persistence.type=hostPath \
  --set persistence.hostPath=/path/to/your/canasta/data
```
