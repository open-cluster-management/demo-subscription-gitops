# Demonstrate BareMetalAssets via Git Ops
## Tool Requirements
- OpenShift CLI Version >= 4.3.0<br>_Needed for kustomize_
```bash
oc version
```

## This repository is set up to manage your Bare Metal Assets as code
### Activate a subscription (ONLY RUN ONCE)
1. Create a branch in the repository or fork the repository.
  - If you branched, update `./subscription/subscription.yaml` and set `apps.open-cluster-management.io/github-branch: master` to your branch name.
  - If you forked the repository, update `./subscription/channel.yaml` and set `spec.pathname` to your forked GitHub repository URL.
2. Create the file `./subscriptions/secret.yaml`.
```yaml
---
apiVersion: v1
kind: Secret
metadata:
  name: my-github-secret
  namespace: baremetal-assets
data:
  user: BASE64_ENCRYPTED_USERNAME
  accessToken: BASE64_ENCRYPTED_PASSWORD
```
  - Base64 encode your git username, and replace `BASE64_ENCRYPED_USERNAME`
  - Base64 encode your git access token, and replace `BASE64_ENCRYPTED_PASSWORD`
3. Add the subscription to your hub cluster.
```
oc apply -k subscription/
```
### Using
- After you have completed the ONE time setup, you will start to see the BMA Objects from the `./bma/BareMetalAssets` folder start appearing in the Bare Metal Asset UI.
- If you commit a change to your branch or forked repo, those changes will appear in the Bare Metal Asset UI in <60s
- The namespace used for the Bare Metal Asset Objects is `default`

