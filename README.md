# regcreds

A Helm chart for creating Docker registry credentials as Kubernetes secrets.

## Installation

Add your registry credentials to your `values.yaml`:

```yaml
pullSecrets:
  - name: example-1
    repository: registry.example.com
    auth:
      username: ""
      password: ""

  - name: example-2
    repository: registry.example.com
    auth:
      username: ""
      password: ""

[...]
```

Then install the chart:

```bash
# Add the GitHub repository as a Helm chart repository
helm repo add regcreds https://majermarci.github.io/regcreds

# Update your local Helm chart repositories
helm repo update

# Install the chart with the values file you made
helm upgrade --install my-regcreds regcreds/regcreds --namespace my-namespace --create-namespace --values values.yaml --set pullSecrets[0].auth.username="name" --set pullSecrets[0].auth.password="pass"

# Or install the chart by passing all values from env vars
helm upgrade --install my-regcreds regcreds/regcreds \
    --namespace my-namespace --create-namespace \
    --set pullSecrets[0].name="example" \
    --set pullSecrets[0].repository="repo.io" \
    --set pullSecrets[0].auth.username="user" \
    --set pullSecrets[0].auth.password="pass"
```

## Usage

Once installed, reference the created secrets in your deployments:

```yaml
imagePullSecrets:
  - name: example-1-regcred
  - name: example-2-regcred
```
