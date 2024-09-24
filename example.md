# Example 1: Basic GitLab Deployment

```yaml
apiVersion: code2cloud.planton.cloud/v1
kind: GitlabKubernetes
metadata:
  name: gitlab-instance
spec:
  kubernetesClusterCredentialId: my-k8s-credentials
  container:
    resources:
      requests:
        cpu: 50m
        memory: 256Mi
      limits:
        cpu: 1
        memory: 1Gi
```

---

# Example 2: GitLab with Ingress Enabled

```yaml
apiVersion: code2cloud.planton.cloud/v1
kind: GitlabKubernetes
metadata:
  name: gitlab-production
spec:
  kubernetesClusterCredentialId: my-k8s-credentials
  container:
    resources:
      requests:
        cpu: 200m
        memory: 512Mi
      limits:
        cpu: 2
        memory: 2Gi
  ingress:
    enabled: true
    hostname: gitlab.example.com
```

---

# Example 3: GitLab Deployment with Custom Resources

```yaml
apiVersion: code2cloud.planton.cloud/v1
kind: GitlabKubernetes
metadata:
  name: gitlab-custom
spec:
  kubernetesClusterCredentialId: my-k8s-credentials
  container:
    resources:
      requests:
        cpu: 500m
        memory: 1Gi
      limits:
        cpu: 3
        memory: 4Gi
```

---

# Example 4: Minimal GitLab Deployment (Empty Spec)

```yaml
apiVersion: code2cloud.planton.cloud/v1
kind: GitlabKubernetes
metadata:
  name: minimal-gitlab
spec:
  kubernetesClusterCredentialId: my-k8s-credentials
```
