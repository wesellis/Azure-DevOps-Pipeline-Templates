# Azure DevOps Pipeline Templates

Professional collection of reusable YAML pipeline templates for Azure DevOps, designed to accelerate CI/CD implementation across multiple technologies and deployment scenarios.

## Table of Contents

- [Overview](#overview)
- [Quick Start](#quick-start)
- [Available Templates](#available-templates)
- [Usage Examples](#usage-examples)
- [Template Parameters](#template-parameters)
- [Best Practices](#best-practices)
- [Contributing](#contributing)
- [License](#license)

## Overview

This repository provides enterprise-ready Azure DevOps pipeline templates that follow industry best practices for:

- **Multi-stage pipelines** with proper separation of build and deploy
- **Parameterized templates** for maximum reusability
- **Security scanning** and code quality checks
- **Artifact management** and deployment strategies
- **Error handling** and comprehensive logging

### Key Features

- **Technology Coverage**: .NET, Node.js, Python, Docker, Kubernetes, Terraform
- **Cloud-Native**: Optimized for Azure services and deployment targets
- **Security-First**: Built-in vulnerability scanning and security best practices
- **Production-Ready**: Comprehensive error handling and rollback strategies
- **Extensible**: Easy to customize and extend for specific requirements

## Quick Start

### 1. Reference Templates in Your Pipeline

```yaml
# azure-pipelines.yml
trigger:
- main

resources:
  repositories:
  - repository: templates
    type: github
    name: wesellis/Azure-DevOps-Pipeline-Templates
    ref: main

extends:
  template: templates/dotnet-build-deploy.yml@templates
  parameters:
    project: '**/*.csproj'
    azureSubscription: 'YourAzureServiceConnection'
    appServiceName: 'your-app-service-name'
    resourceGroupName: 'your-resource-group'
```

### 2. Using Multiple Templates

```yaml
# Complex pipeline using multiple templates
stages:
- template: templates/dotnet-build-deploy.yml@templates
  parameters:
    project: 'src/WebApp/*.csproj'
    azureSubscription: 'AzureConnection'
    appServiceName: 'webapp-prod'
    resourceGroupName: 'webapp-rg'

- template: templates/terraform-init-apply.yml@templates
  parameters:
    workingDirectory: 'infrastructure/'
    backendServiceConnection: 'TerraformBackend'
    environmentServiceConnection: 'AzureConnection'
    backendResourceGroupName: 'tfstate-rg'
    backendStorageAccountName: 'tfstatestorage'
    backendKey: 'webapp.tfstate'
```

## Available Templates

| Template | Technology | Purpose | Status |
|----------|------------|---------|--------|
| **dotnet-build-deploy.yml** | .NET | Build and deploy .NET applications to Azure App Service | ✅ Ready |
| **node-build-deploy.yml** | Node.js | Build and deploy Node.js applications with npm/yarn/pnpm | ✅ Ready |
| **python-build-deploy.yml** | Python | Build and deploy Python applications | 🔧 In Progress |
| **docker-build-push.yml** | Docker | Build and push Docker images to container registries | ✅ Ready |
| **k8s-deploy.yml** | Kubernetes | Deploy applications to Kubernetes clusters | ✅ Ready |
| **terraform-init-apply.yml** | Terraform | Initialize and apply Terraform infrastructure | ✅ Ready |
| **arm-deploy.yml** | ARM Templates | Deploy Azure Resource Manager templates | 🔧 In Progress |

## Usage Examples

### .NET Application Deployment

```yaml
extends:
  template: templates/dotnet-build-deploy.yml
  parameters:
    project: 'src/**/*.csproj'
    buildConfiguration: 'Release'
    dotnetVersion: '8.x'
    azureSubscription: 'Production-ServiceConnection'
    appServiceName: 'myapp-prod'
    resourceGroupName: 'myapp-rg'
    runTests: true
```

### Docker Multi-Architecture Build

```yaml
extends:
  template: templates/docker-build-push.yml
  parameters:
    dockerFile: 'Dockerfile'
    containerRegistry: 'myregistry.azurecr.io'
    repository: 'myapp'
    tag: '$(Build.BuildNumber)'
    additionalTags:
    - 'latest'
    - 'v1.0'
    buildArgs:
    - 'BUILD_VERSION=$(Build.BuildNumber)'
    - 'BUILD_DATE=$(Build.Date)'
    scanImage: true
```

### Kubernetes Blue-Green Deployment

```yaml
extends:
  template: templates/k8s-deploy.yml
  parameters:
    kubernetesServiceConnection: 'K8s-Cluster'
    namespace: 'production'
    deploymentManifests: 'k8s/production/*.yml'
    repository: 'myregistry.azurecr.io/myapp'
    imageTag: '$(Build.BuildNumber)'
    replicas: 5
    strategy: 'blue-green'
    healthCheckPath: '/api/health'
    runSmokeTests: true
```

### Infrastructure as Code

```yaml
extends:
  template: templates/terraform-init-apply.yml
  parameters:
    terraformVersion: '1.5.0'
    workingDirectory: 'terraform/'
    backendServiceConnection: 'TerraformStorage'
    environmentServiceConnection: 'AzureProd'
    backendResourceGroupName: 'terraform-state-rg'
    backendStorageAccountName: 'terraformstatestorage'
    backendContainerName: 'tfstate'
    backendKey: 'infrastructure/prod.tfstate'
    planOnly: false
    additionalArgs: '-var-file="environments/prod.tfvars"'
```

## Template Parameters

### Common Parameters

Most templates support these common parameters:

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `azureSubscription` | string | - | Azure service connection name |
| `resourceGroupName` | string | - | Target resource group |
| `buildConfiguration` | string | 'Release' | Build configuration (Debug/Release) |
| `runTests` | boolean | true | Whether to execute tests |
| `environmentVariables` | object | [] | Environment variables for deployment |

### Template-Specific Parameters

#### .NET Template
- `project`: Project file pattern (default: '**/*.csproj')
- `dotnetVersion`: .NET SDK version (default: '8.x')
- `publishProfile`: Optional publish profile
- `appServiceName`: Azure App Service name

#### Docker Template
- `dockerFile`: Dockerfile path (default: 'Dockerfile')
- `containerRegistry`: Container registry service connection
- `repository`: Image repository name
- `buildArgs`: Docker build arguments
- `scanImage`: Enable vulnerability scanning

#### Kubernetes Template
- `kubernetesServiceConnection`: Kubernetes cluster connection
- `namespace`: Target namespace (default: 'default')
- `deploymentManifests`: Kubernetes manifest files
- `replicas`: Number of replicas (default: 3)
- `healthCheckPath`: Health check endpoint

#### Terraform Template
- `terraformVersion`: Terraform version (default: 'latest')
- `workingDirectory`: Terraform files directory
- `backendServiceConnection`: Azure backend connection
- `planOnly`: Only run plan, don't apply
- `destroyMode`: Run terraform destroy

## Best Practices

### Template Usage
- **Pin template versions** using specific tags or commits
- **Test templates** in non-production environments first
- **Use parameter files** for environment-specific configurations
- **Implement proper secret management** using Azure Key Vault

### Pipeline Security
- **Use service connections** instead of hardcoded credentials
- **Enable branch protection** for production deployments
- **Implement approval gates** for critical environments
- **Scan for vulnerabilities** in all build artifacts

### Performance Optimization
- **Use pipeline caching** for dependencies and build outputs
- **Parallelize independent jobs** where possible
- **Optimize Docker builds** with multi-stage builds and layer caching
- **Monitor pipeline performance** and optimize bottlenecks

## Advanced Configuration

### Custom Extensions

```yaml
# Extending templates with custom steps
extends:
  template: templates/dotnet-build-deploy.yml
  parameters:
    project: '**/*.csproj'
    # Standard parameters...
    
# Add custom pre-deployment steps
- stage: CustomPreDeploy
  displayName: 'Custom Pre-Deployment Tasks'
  dependsOn: Build
  jobs:
  - job: DatabaseMigration
    # Custom database migration logic
```

### Environment-Specific Overrides

```yaml
# Using parameter files for different environments
- ${{ if eq(variables['Build.SourceBranch'], 'refs/heads/main') }}:
  - template: templates/dotnet-build-deploy.yml
    parameters:
      azureSubscription: 'Production-Connection'
      appServiceName: 'myapp-prod'
      
- ${{ if eq(variables['Build.SourceBranch'], 'refs/heads/develop') }}:
  - template: templates/dotnet-build-deploy.yml
    parameters:
      azureSubscription: 'Development-Connection'
      appServiceName: 'myapp-dev'
```

## Troubleshooting

### Common Issues

#### Template Not Found
```yaml
# Ensure repository reference is correct
resources:
  repositories:
  - repository: templates
    type: github
    name: wesellis/Azure-DevOps-Pipeline-Templates
    ref: main  # or specific tag/commit
```

#### Parameter Validation Errors
- Check parameter types match template expectations
- Verify required parameters are provided
- Use proper YAML syntax for arrays and objects

#### Service Connection Issues
- Verify service connection names exist in Azure DevOps
- Check service connection permissions
- Ensure service principal has required Azure RBAC roles

### Getting Help

1. **Check the documentation** for template-specific requirements
2. **Review parameter examples** in this README
3. **Open an issue** for bugs or feature requests
4. **Contribute improvements** via pull requests

## Contributing

We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details on:

- Adding new templates
- Improving existing templates
- Documentation updates
- Testing procedures
- Code review process

### Development Setup

```bash
# Clone the repository
git clone https://github.com/wesellis/Azure-DevOps-Pipeline-Templates.git
cd Azure-DevOps-Pipeline-Templates

# Create a feature branch
git checkout -b feature/new-template

# Make your changes and test
# Submit a pull request
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

For support and questions:
- **Email**: wes@wesellis.com
- **Issues**: GitHub Issues for bugs and feature requests
- **Discussions**: GitHub Discussions for questions and ideas

---

**Professional Azure DevOps Pipeline Templates** | Making CI/CD implementation faster and more reliable
