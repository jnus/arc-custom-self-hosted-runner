# arc-custom-self-hosted-runner
Custom docker image for GitHub self hosted runners running in ARC

# PAT ghcr.io authentication
```
export CR_PAT=ghp_***
echo $CR_PAT | docker login ghcr.io -u USERNAME --password-stdin
```

# Build  docker images
```
# Basic arc image
docker build --platform linux/amd64 -t arc-basic-runner ./images/.
docker tag arc-basic-runner ghcr.io/jnus/arc-basic-runner
docker push ghcr.io/jnus/arc-basic-runner
```

# Runner set with basic runner image
```
INSTALLATION_NAME="arc-runner-set-basic"
NAMESPACE="arc-runners"
GITHUB_CONFIG_URL="https://github.com/jnusorg"
helm install "${INSTALLATION_NAME}" \
    --namespace "${NAMESPACE}" \
    --create-namespace \
    -f /Users/jnus/git/arc-custom-self-hosted-runner/charts/arc-basic-runner/values.yml \
    oci://ghcr.io/actions/actions-runner-controller-charts/gha-runner-scale-set
```