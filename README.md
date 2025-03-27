# regcreds

A Helm chart for creating Docker registry credentials as Kubernetes secrets.

## Installation

Add your registry credentials to `values.yaml`:

```yaml
pullSecrets:
  - name: example
    repository: registry.example.com
    auth:
      username: my-username
      password: my-password
      email: my-email@example.com

  - name: other-example
    repository: registry.example.io
    auth:
      username: my-username
      password: my-password
      email: my-email@example.com
```

Then install the chart:

```bash
# Add the GitHub repository as a Helm chart repository
helm repo add regcreds https://majermarci.github.io/regcreds

# Update your local Helm chart repositories
helm repo update

# Install the chart
helm upgrade --install my-regcreds regcreds/regcreds -n my-namespace --create-namespace
```

## Usage

Once installed, reference the created secrets in your deployments:

```yaml
imagePullSecrets:
  - name: example-regcred
  - name: other-example-regcred
```
