# regcreds

A Helm chart for creating Docker registry credentials as Kubernetes secrets.

## Installation

Add your registry credentials to your `values.yaml`:

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
helm upgrade --install my-regcreds regcreds/regcreds -n my-namespace --create-namespace --values values.yaml

# Or install the chart by passing values from env vars
helm template my-regcreds regcreds/regcreds \
    --namespace my-namespace --create-namespace \
    --set pullSecrets[0].name="example" \
    --set pullSecrets[0].repository="repo.io" \
    --set pullSecrets[0].auth.username="user" \
    --set pullSecrets[0].auth.password="pass" \
    --set pullSecrets[0].auth.email="email@example.com"
```

## Usage

Once installed, reference the created secrets in your deployments:

```yaml
imagePullSecrets:
  - name: example-regcred
  - name: other-example-regcred
```
