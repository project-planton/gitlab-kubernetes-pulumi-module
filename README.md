# GitLab Kubernetes Pulumi Module

## Key Features

- **Declarative Deployment**: The module leverages Planton Cloud’s unified API structure to allow users to specify their GitLab configuration declaratively. This ensures consistency in deployments across multiple environments.

- **Kubernetes Native Integration**: The module is tightly integrated with Kubernetes, provisioning namespaces, services, and ingress resources. This ensures that all necessary components for GitLab are correctly set up within your Kubernetes cluster.

- **Customizable Resource Management**: Users can define container resource requests and limits (CPU and memory) for the GitLab instance. This provides granular control over resource allocation, allowing GitLab to be tailored to different performance and resource consumption requirements.

- **Ingress Support**: The module provides the option to configure ingress, enabling external access to GitLab through custom hostnames and TLS certificates. This ensures that the GitLab instance can be securely accessed from outside the cluster if required.

- **Port-Forwarding for Secure Access**: In cases where ingress is disabled for security reasons, the module offers port-forwarding commands, allowing developers to access the GitLab instance from their local machine. This feature is particularly useful for secure, internal-only deployments of GitLab.

- **Seamless Pulumi Integration**: The module is fully integrated with Pulumi, allowing infrastructure to be managed as code. It handles the lifecycle of the GitLab deployment, ensuring that changes to the API resource are automatically reflected in the infrastructure.

- **Automated Namespace Management**: The module creates or reuses Kubernetes namespaces for GitLab, ensuring that each instance is properly isolated from other workloads within the cluster.

- **Outputs for Monitoring and Access**: The module captures important details about the deployment, including:
  - The namespace where GitLab is deployed.
  - The Kubernetes service name used to expose GitLab.
  - Commands for port-forwarding access to GitLab when ingress is disabled.
  - Kubernetes internal and external endpoints for accessing GitLab.
  - Ingress endpoints for public or internal access, if ingress is enabled.

## Usage

To deploy GitLab using this module, create a `GitlabKubernetes` YAML file that defines the desired configuration. Once the YAML file is prepared, you can deploy the GitLab instance using the following command:

```bash
planton pulumi up --stack-input <api-resource.yaml>
```

Refer to the **Examples** section for detailed usage instructions.

## Pulumi Integration

This module is built using Pulumi's Go SDK, providing deep integration with Kubernetes. The module processes the `GitlabKubernetes` API resource and provisions the necessary Kubernetes components based on the declarative specification provided in the YAML file. Pulumi ensures that changes to the API resource are automatically applied to the infrastructure, simplifying updates and scaling operations.

### Key Pulumi Components

1. **Kubernetes Provider**: The module sets up the Kubernetes provider using the `kubernetes_cluster_credential_id` provided in the API resource, ensuring that all resources are created within the correct cluster.

2. **Namespace Management**: A Kubernetes namespace is automatically created or reused, based on the `metadata.name` field, isolating the GitLab resources from other workloads within the cluster.

3. **Kubernetes Services**: The module creates Kubernetes services that expose GitLab, either within the cluster or externally, based on the provided configuration.

4. **Ingress Configuration**: If enabled, ingress is set up to expose GitLab to external traffic. The module supports defining custom hostnames and TLS certificates for secure access.

5. **Port-Forwarding**: For cases where ingress is disabled, the module generates port-forwarding commands to allow secure local access to GitLab via `kubectl`. This ensures developers can interact with GitLab without exposing it to external networks.

6. **Resource Requests and Limits**: Users can define resource requests and limits for GitLab’s container, controlling the CPU and memory allocation. This ensures that GitLab operates efficiently within the available cluster resources.

7. **Output Management**: After deployment, the module exports key details of the infrastructure, including:
   - The namespace where GitLab is deployed.
   - The service name used to access GitLab within the Kubernetes cluster.
   - Port-forwarding commands for accessing GitLab locally when ingress is disabled.
   - Internal and external endpoints for accessing GitLab.
   - Ingress endpoints (if enabled) for accessing GitLab from outside the cluster.

## Status and Monitoring

All outputs from the Pulumi deployment are stored in the `status.stackOutputs` field. These outputs provide essential information for monitoring and accessing the GitLab instance, including service names, port-forwarding commands, and ingress endpoints. This ensures that all critical details about the deployment are easily accessible for ongoing management.

## Conclusion

The `gitlab-kubernetes-pulumi-module` offers a streamlined and powerful way to deploy GitLab in Kubernetes clusters. By adopting a declarative approach and leveraging Pulumi’s infrastructure-as-code capabilities, this module simplifies the provisioning, management, and scaling of GitLab. Whether for small or large-scale deployments, this module ensures that GitLab is deployed consistently, securely, and efficiently across different environments.