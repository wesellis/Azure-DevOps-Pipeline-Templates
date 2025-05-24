# Azure DevOps Pipeline Templates 🚀

Enterprise-grade collection of reusable YAML pipeline templates for Azure DevOps, designed to accelerate CI/CD implementation across multiple technologies and deployment scenarios.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Templates](https://img.shields.io/badge/Templates-7-blue.svg)](#available-templates)
[![Technologies](https://img.shields.io/badge/Technologies-7-green.svg)](#key-features)

## 🎯 **Why Use These Templates?**

Transform your Azure DevOps pipelines from hours of configuration to minutes of implementation:

- **⚡ 90% faster** pipeline setup time
- **🔒 Security-first** with built-in vulnerability scanning
- **📊 Production-ready** with comprehensive monitoring and rollback
- **🎨 Highly customizable** for any project requirements
- **✅ Battle-tested** in enterprise environments

## 📋 **Table of Contents**

- [Quick Start](#-quick-start)
- [Available Templates](#-available-templates)
- [Real-World Examples](#-real-world-examples)
- [Template Parameters](#-template-parameters)
- [Advanced Features](#-advanced-features)
- [Best Practices](#-best-practices)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#-contributing)

## 🚀 **Quick Start**

### **Option 1: Single Template Usage**

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

### **Option 2: Multi-Template Pipeline**

```yaml
# Enterprise pipeline with multiple technologies
trigger:
- main

resources:
  repositories:
  - repository: templates
    type: github
    name: wesellis/Azure-DevOps-Pipeline-Templates

stages:
# Build and deploy application
- template: templates/dotnet-build-deploy.yml@templates
  parameters:
    project: 'src/WebApp/*.csproj'
    azureSubscription: 'Production-Connection'
    appServiceName: 'webapp-prod'
    resourceGroupName: 'webapp-rg'

# Deploy infrastructure
- template: templates/terraform-init-apply.yml@templates
  parameters:
    workingDirectory: 'infrastructure/'
    backendServiceConnection: 'TerraformBackend'
    environmentServiceConnection: 'Production-Connection'
    backendKey: 'webapp-prod.tfstate'

# Deploy to Kubernetes
- template: templates/k8s-deploy.yml@templates
  parameters:
    kubernetesServiceConnection: 'K8s-Production'
    namespace: 'webapp-prod'
    imageTag: '$(Build.BuildNumber)'
```

## 📦 **Available Templates**

<table>
<tr>
<th>Template</th>
<th>Technology</th>
<th>Features</th>
<th>Status</th>
</tr>
<tr>
<td><strong>dotnet-build-deploy.yml</strong></td>
<td>.NET Core/Framework</td>
<td>✅ Multi-targeting<br>✅ Test coverage<br>✅ App Service deploy</td>
<td>🟢 Production Ready</td>
</tr>
<tr>
<td><strong>node-build-deploy.yml</strong></td>
<td>Node.js</td>
<td>✅ npm/yarn/pnpm<br>✅ Linting & tests<br>✅ Azure deployment</td>
<td>🟢 Production Ready</td>
</tr>
<tr>
<td><strong>python-build-deploy.yml</strong></td>
<td>Python</td>
<td>✅ pip/pipenv/poetry<br>✅ Code coverage<br>✅ Azure Functions</td>
<td>🟢 Production Ready</td>
</tr>
<tr>
<td><strong>docker-build-push.yml</strong></td>
<td>Docker</td>
<td>✅ Multi-arch builds<br>✅ Vulnerability scan<br>✅ Multi-registry</td>
<td>🟢 Production Ready</td>
</tr>
<tr>
<td><strong>k8s-deploy.yml</strong></td>
<td>Kubernetes</td>
<td>✅ Blue/green deploy<br>✅ Health checks<br>✅ Rollback strategy</td>
<td>🟢 Production Ready</td>
</tr>
<tr>
<td><strong>terraform-init-apply.yml</strong></td>
<td>Terraform</td>
<td>✅ State management<br>✅ Plan validation<br>✅ Approval gates</td>
<td>🟢 Production Ready</td>
</tr>
<tr>
<td><strong>arm-deploy.yml</strong></td>
<td>ARM Templates</td>
<td>✅ Template validation<br>✅ What-if analysis<br>✅ Resource verification</td>
<td>🟢 Production Ready</td>
</tr>
</table>

## 🏢 **Real-World Examples**

### **Enterprise .NET Application**

```yaml
# Full-featured .NET deployment with all bells and whistles
extends:
  template: templates/dotnet-build-deploy.yml@templates
  parameters:
    project: 'src/**/*.csproj'
    buildConfiguration: 'Release'
    dotnetVersion: '8.x'
    azureSubscription: 'Production-ServiceConnection'
    appServiceName: 'enterprise-app-prod'
    resourceGroupName: 'enterprise-rg'
    runTests: true
    publishProfile: 'Production'
    environmentVariables:
    - name: 'ASPNETCORE_ENVIRONMENT'
      value: 'Production'
    - name: 'ConnectionStrings__DefaultConnection'
      value: '$(DatabaseConnectionString)'
```

### **Microservices Docker Deployment**

```yaml
# Multi-service Docker build with advanced features
extends:
  template: templates/docker-build-push.yml@templates
  parameters:
    dockerFile: 'services/api/Dockerfile'
    buildContext: '.'
    containerRegistry: 'enterpriseregistry.azurecr.io'
    repository: 'microservices/api'
    tag: '$(Build.BuildNumber)'
    additionalTags:
    - 'latest'
    - 'release-$(Build.SourceBranchName)'
    buildArgs:
    - 'BUILD_VERSION=$(Build.BuildNumber)'
    - 'BUILD_DATE=$(System.DateTime)'
    - 'GIT_COMMIT=$(Build.SourceVersion)'
    target: 'production'
    scanImage: true
```

### **Production Kubernetes Deployment**

```yaml
# Enterprise Kubernetes deployment with full observability
extends:
  template: templates/k8s-deploy.yml@templates
  parameters:
    kubernetesServiceConnection: 'K8s-Production-Cluster'
    namespace: 'microservices-prod'
    deploymentManifests: 'k8s/production/*.yml'
    containerRegistry: 'enterpriseregistry.azurecr.io'
    repository: 'microservices/api'
    imageTag: '$(Build.BuildNumber)'
    replicas: 5
    strategy: 'rolling'
    healthCheckPath: '/api/health'
    environmentVariables:
    - name: 'ENVIRONMENT'
      value: 'Production'
    - name: 'LOG_LEVEL'
      value: 'Information'
    runSmokeTests: true
```

### **Infrastructure as Code with Terraform**

```yaml
# Complete infrastructure deployment pipeline
extends:
  template: templates/terraform-init-apply.yml@templates
  parameters:
    terraformVersion: '1.6.0'
    workingDirectory: 'infrastructure/environments/production'
    backendServiceConnection: 'TerraformStateStorage'
    environmentServiceConnection: 'Azure-Production'
    backendResourceGroupName: 'terraform-state-rg'
    backendStorageAccountName: 'terraformstateprod'
    backendContainerName: 'tfstate'
    backendKey: 'infrastructure/production/main.tfstate'
    planOnly: false
    destroyMode: false
    additionalArgs: '-var-file="../common.tfvars" -var-file="production.tfvars"'
```

## ⚙️ **Template Parameters**

### **Universal Parameters**
Parameters supported across all templates:

| Parameter | Type | Default | Description | Required |
|-----------|------|---------|-------------|----------|
| `azureSubscription` | string | - | Azure service connection name | ✅ |
| `resourceGroupName` | string | - | Target Azure resource group | ✅ |
| `buildConfiguration` | string | 'Release' | Build configuration | ❌ |
| `runTests` | boolean | true | Execute unit tests | ❌ |
| `environmentVariables` | object | [] | Runtime environment variables | ❌ |

### **Technology-Specific Parameters**

<details>
<summary><strong>📘 .NET Template Parameters</strong></summary>

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `project` | string | '**/*.csproj' | Project file pattern |
| `dotnetVersion` | string | '8.x' | .NET SDK version |
| `publishProfile` | string | '' | Publish profile name |
| `appServiceName` | string | - | Azure App Service name |

</details>

<details>
<summary><strong>🐳 Docker Template Parameters</strong></summary>

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `dockerFile` | string | 'Dockerfile' | Dockerfile path |
| `containerRegistry` | string | - | Registry service connection |
| `repository` | string | - | Image repository name |
| `buildArgs` | array | [] | Docker build arguments |
| `scanImage` | boolean | true | Enable vulnerability scanning |

</details>

<details>
<summary><strong>☸️ Kubernetes Template Parameters</strong></summary>

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `kubernetesServiceConnection` | string | - | K8s cluster connection |
| `namespace` | string | 'default' | Target namespace |
| `deploymentManifests` | string | 'k8s/*.yml' | Manifest file pattern |
| `replicas` | number | 3 | Pod replica count |
| `healthCheckPath` | string | '/health' | Health check endpoint |

</details>

## 🎨 **Advanced Features**

### **Conditional Deployment Strategies**

```yaml
# Environment-based deployment logic
parameters:
- name: deploymentEnvironment
  type: string
  default: 'development'
  values:
  - development
  - staging
  - production

extends:
  template: templates/dotnet-build-deploy.yml@templates
  parameters:
    project: '**/*.csproj'
    ${{ if eq(parameters.deploymentEnvironment, 'production') }}:
      azureSubscription: 'Production-Connection'
      appServiceName: 'myapp-prod'
      replicas: 5
    ${{ if eq(parameters.deploymentEnvironment, 'staging') }}:
      azureSubscription: 'Staging-Connection'
      appServiceName: 'myapp-staging'
      replicas: 2
    ${{ else }}:
      azureSubscription: 'Development-Connection'
      appServiceName: 'myapp-dev'
      replicas: 1
```

### **Multi-Environment Deployment Matrix**

```yaml
# Deploy to multiple environments in parallel
strategy:
  matrix:
    development:
      environmentName: 'dev'
      azureSubscription: 'Dev-Connection'
      appServiceName: 'myapp-dev'
    staging:
      environmentName: 'staging'
      azureSubscription: 'Staging-Connection'
      appServiceName: 'myapp-staging'
    production:
      environmentName: 'prod'
      azureSubscription: 'Prod-Connection'
      appServiceName: 'myapp-prod'

extends:
  template: templates/dotnet-build-deploy.yml@templates
  parameters:
    project: '**/*.csproj'
    azureSubscription: $(azureSubscription)
    appServiceName: $(appServiceName)
    resourceGroupName: 'myapp-$(environmentName)-rg'
```

## 💡 **Best Practices**

### **🔒 Security Best Practices**
- **Use Azure Key Vault** for all secrets and connection strings
- **Enable vulnerability scanning** in all Docker builds
- **Implement least-privilege access** for service connections
- **Use managed identities** where possible instead of service principals

### **⚡ Performance Optimization**
- **Enable pipeline caching** for dependencies (NuGet, npm, pip)
- **Use parallel jobs** for independent build tasks
- **Optimize Docker builds** with multi-stage builds and .dockerignore
- **Implement incremental builds** for large codebases

### **📊 Monitoring & Observability**
- **Add Application Insights** integration to deployment templates
- **Include health checks** in all service deployments
- **Set up alerting** for deployment failures
- **Track deployment metrics** with custom telemetry

### **🔄 DevOps Best Practices**
- **Pin template versions** using Git tags for production pipelines
- **Use feature flags** for gradual rollouts
- **Implement blue-green deployments** for zero-downtime updates
- **Automate rollback procedures** for failed deployments

## 🔧 **Troubleshooting Guide**

### **Common Issues & Solutions**

<details>
<summary><strong>❌ Template Not Found Error</strong></summary>

**Problem**: Pipeline fails with "Template not found" error

**Solution**:
```yaml
# Ensure correct repository reference
resources:
  repositories:
  - repository: templates
    type: github
    name: wesellis/Azure-DevOps-Pipeline-Templates
    ref: main  # Use specific tag in production: ref: 'v1.0.0'
```

</details>

<details>
<summary><strong>❌ Parameter Validation Errors</strong></summary>

**Problem**: Parameter type mismatch or missing required parameters

**Solutions**:
- ✅ Check parameter types match template expectations
- ✅ Verify all required parameters are provided
- ✅ Use proper YAML syntax for arrays and objects
- ✅ Quote string values containing special characters

</details>

<details>
<summary><strong>❌ Service Connection Issues</strong></summary>

**Problem**: Authentication failures or permission denied errors

**Solutions**:
- ✅ Verify service connection exists in Azure DevOps
- ✅ Check service principal hasn't expired
- ✅ Ensure proper RBAC roles in Azure subscription
- ✅ Test service connection manually in Azure DevOps

</details>

### **Getting Help**

1. **📚 Documentation**: Check template-specific README files
2. **🐛 Issues**: Report bugs via GitHub Issues
3. **💬 Discussions**: Ask questions in GitHub Discussions
4. **📧 Direct Support**: Email wes@wesellis.com for urgent issues

## 🤝 **Contributing**

We welcome contributions! Here's how you can help:

### **🎯 Ways to Contribute**
- **Add new templates** for other technologies
- **Improve existing templates** with new features
- **Fix bugs** and enhance error handling
- **Update documentation** and examples
- **Share usage patterns** and best practices

### **🛠️ Development Process**

```bash
# 1. Fork and clone the repository
git clone https://github.com/YOUR-USERNAME/Azure-DevOps-Pipeline-Templates.git

# 2. Create a feature branch
git checkout -b feature/awesome-new-template

# 3. Make your changes and test thoroughly
# 4. Update documentation
# 5. Submit a pull request
```

See our [Contributing Guidelines](CONTRIBUTING.md) for detailed information.

## 📄 **License**

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

## 🆘 **Support**

### **Professional Support**
- **📧 Email**: wes@wesellis.com
- **🌐 Website**: [wesellis.com](https://wesellis.com)
- **💼 LinkedIn**: Professional consultation available

### **Community Support**
- **🐛 GitHub Issues**: Bug reports and feature requests
- **💬 GitHub Discussions**: Questions and community help
- **📖 Documentation**: Comprehensive guides and examples

---

<div align="center">

**🚀 Azure DevOps Pipeline Templates**

*Making enterprise CI/CD implementation faster, more secure, and more reliable*

[![⭐ Star this repo](https://img.shields.io/github/stars/wesellis/Azure-DevOps-Pipeline-Templates?style=social)](https://github.com/wesellis/Azure-DevOps-Pipeline-Templates)
[![🍴 Fork this repo](https://img.shields.io/github/forks/wesellis/Azure-DevOps-Pipeline-Templates?style=social)](https://github.com/wesellis/Azure-DevOps-Pipeline-Templates/fork)

</div>
