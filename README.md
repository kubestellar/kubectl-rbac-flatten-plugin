# kubectl-rbac-flatten-plugin

A kubectl plugin that flattens RBAC roles, cluster roles, and their associated bindings to simplify Kubernetes RBAC management.

## Overview

The `kubectl-rbac-flatten` plugin analyzes and consolidates Kubernetes RBAC (Role-Based Access Control) resources, making it easier to understand and manage permissions across multiple subjects. By flattening the RBAC hierarchy, this tool enables better visibility into access patterns and facilitates centralized RBAC policy management.

## Features

- **Flatten Roles and ClusterRoles**: Consolidate multiple role definitions into a simplified view
- **Flatten RoleBindings and ClusterRoleBindings**: Merge bindings to show comprehensive access mappings
- **Subject Consolidation**: Group permissions by subjects (users, groups, service accounts)
- **Improved RBAC Visibility**: Better understanding of who has access to what resources
- **Policy Management**: Simplify the process of auditing and managing RBAC policies

## Prerequisites

- Kubernetes cluster (v1.19+)
- kubectl installed and configured
- Appropriate permissions to read RBAC resources in your cluster

## Installation

### Using Krew (Recommended)

_Note: Krew distribution is planned for a future release. Until then, please use manual installation or build from source._

Once available, you'll be able to install via [Krew](https://krew.sigs.k8s.io/):
```bash
kubectl krew install rbac-flatten
```

### Manual Installation

_Note: Pre-built releases will be available once the first version is published._

1. Download the latest release from the [releases page](https://github.com/kubestellar/kubectl-rbac-flatten-plugin/releases) (when available)
2. Extract the binary and place it in your PATH:
   ```bash
   tar -xzf kubectl-rbac-flatten-*.tar.gz
   sudo mv kubectl-rbac-flatten /usr/local/bin/
   sudo chmod +x /usr/local/bin/kubectl-rbac-flatten
   ```
3. Verify the installation:
   ```bash
   kubectl rbac-flatten --help
   ```

### Build from Source

```bash
# Clone the repository
git clone https://github.com/kubestellar/kubectl-rbac-flatten-plugin.git
cd kubectl-rbac-flatten-plugin

# Build the plugin
go build -o kubectl-rbac-flatten

# Move to PATH
sudo mv kubectl-rbac-flatten /usr/local/bin/
```

## Usage

### Basic Commands

```bash
# Flatten all roles in the current namespace
kubectl rbac-flatten roles

# Flatten all cluster roles
kubectl rbac-flatten clusterroles

# Flatten role bindings for a specific namespace
kubectl rbac-flatten rolebindings -n <namespace>

# Flatten cluster role bindings
kubectl rbac-flatten clusterrolebindings

# Flatten all RBAC resources
kubectl rbac-flatten all
```

### Examples

**View flattened permissions for a specific subject:**
```bash
kubectl rbac-flatten --subject user:john@example.com
```

**Export flattened RBAC to a file:**
```bash
kubectl rbac-flatten all --output yaml > flattened-rbac.yaml
```

**Filter by namespace:**
```bash
kubectl rbac-flatten roles -n kube-system
```

## Configuration Options

| Flag | Description | Default |
|------|-------------|---------|
| `--namespace, -n` | Specify namespace | current context namespace |
| `--all-namespaces, -A` | Show resources across all namespaces | false |
| `--output, -o` | Output format (yaml, json, table) | table |
| `--subject` | Filter by subject (user, group, serviceaccount) | - |
| `--verbose, -v` | Enable verbose output | false |

## Development

### Prerequisites for Development

- Go 1.20 or later
- kubectl
- Access to a Kubernetes cluster for testing

### Building

```bash
# Build the plugin
make build

# Run tests
make test

# Run linting
make lint
```

### Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

Please ensure:
- Code follows Go best practices
- Tests are included for new features
- Documentation is updated as needed

## Use Cases

- **Security Audits**: Quickly identify and review all permissions granted to specific subjects
- **RBAC Cleanup**: Identify redundant or conflicting role assignments
- **Compliance**: Generate reports on access controls for compliance requirements
- **Troubleshooting**: Debug permission issues by viewing consolidated access rights
- **Migration**: Simplify RBAC during cluster migrations or reorganizations

## Roadmap

- [ ] Initial release with basic flattening functionality
- [ ] Support for output formats (YAML, JSON, table)
- [ ] Advanced filtering and querying capabilities
- [ ] Krew plugin distribution
- [ ] Visual graph representation of RBAC relationships
- [ ] Diff mode to compare RBAC configurations
- [ ] Policy validation and recommendations

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

## Support

- **Issues**: Report bugs or request features via [GitHub Issues](https://github.com/kubestellar/kubectl-rbac-flatten-plugin/issues)
- **Discussions**: Join the conversation in [GitHub Discussions](https://github.com/kubestellar/kubectl-rbac-flatten-plugin/discussions)
- **KubeStellar Community**: Visit [kubestellar.io](https://kubestellar.io) for more information about the KubeStellar project

## Acknowledgments

This plugin is part of the [KubeStellar](https://github.com/kubestellar) project ecosystem, which focuses on multi-cluster management and control plane solutions for Kubernetes.
